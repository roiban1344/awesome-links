# Links
- [Fullstack app with TypeScript, Next\.js, Prisma & GraphQL](https://www.prisma.io/blog/fullstack-nextjs-graphql-prisma-oklidw1rhw)

- [How to Build a Fullstack App with Next\.js, Prisma, and PostgreSQL – Vercel Docs](https://vercel.com/guides/nextjs-prisma-postgres)

- [How to set up a free PostgreSQL database on Heroku \- DEV Community 👩‍💻👨‍💻](https://dev.to/prisma/how-to-setup-a-free-postgresql-database-on-heroku-1dc1)

## Prisma
紹介ページ
- [Prisma Client \- Auto\-generated query builder for your data](https://www.prisma.io/client)
- [Prisma Migrate \| Hassle\-free Database Migrations](https://www.prisma.io/migrate)

APIリファレンス
- [Prisma schema \(Reference\) \| Prisma Docs](https://www.prisma.io/docs/concepts/components/prisma-schema)
- [Prisma Client API \(Reference\) \| Prisma Docs](https://www.prisma.io/docs/reference/api-reference/prisma-client-reference)


# 作業メモ
## prisma初期設定
`prisma`を
```
npm install prisma -D
```
でdependenciesに追加。さらに
```
$ npx prisma init
3. Run prisma db pull to turn your database schema into a Prisma schema.
4. Run prisma generate to generate the Prisma Client. You can then start querying your database.

More information in our documentation:
https://pris.ly/d/getting-started
```
で`/prisma/schema.prisma`の雛形と`.env`が生成される。

`.env`ファイルにはHerokuに立てたデータベースのURLをコピー。

Appの個別ページを開いて、 

Resources &gt; Heroku Postgres &gt; Settings &gt; Database Credentials (View Credentials)&gt; URI

から参照。

## モデル定義
モデルに
```
model User{
    //略
    bookmarks Link[]
}

model Link{
    //略
    users User[]
}
```

のように書くとmany-to-many(m-n) relation が暗黙的に定義され、対応するテーブルが用意される。

[Relations \(Reference\) \| Prisma Docs](https://www.prisma.io/docs/concepts/components/prisma-schema/relations)

## マイグレーション
```
npx prisma db push
```
でHeroku Postgres上に3つのテーブルが作成される。

# シーディング
- Conventioalにはprisma/seed.tsにシード用ファイルを配置する。
- `--preview-feature`オプションは現在は不要。
- package.jsonのの`scripts`の`ts-node`プロパティは廃止されている。
- Next.jsはデフォルトではESNextモジュールを使うため、`seed`コマンドの実行には設定が必要。以下をpackage.jsonに追記。
```
  "prisma": {
    "seed": "ts-node --compiler-options {\"module\":\"CommonJS\"} prisma/seed.ts"
  },
```
そうしないと以下のエラーを得る。
```
$ npx prisma db seed --preview-feature
Environment variables loaded from .env
prisma:warn Prisma "db seed" was in Preview and is now Generally Available.
You can now remove the --preview-feature flag.
Error: To configure seeding in your project you need to add a "prisma.seed" property in your package.json with the command to execute it:

1. Open the package.json of your project
2. Add one of the following examples to your package.json:

TypeScript:
```
"prisma": {
  "seed": "ts-node ./prisma/seed.ts"
}
```
If you are using ESM (ECMAScript modules):
```
"prisma": {
  "seed": "node --loader ts-node/esm ./prisma/seed.ts"
}
```

And install the required dependencies by running:
npm i -D ts-node typescript @types/node

JavaScript:
```
"prisma": {
  "seed": "node ./prisma/seed.js"
}
```

Bash:
```
"prisma": {
  "seed": "./prisma/seed.sh"
}
```
And run `chmod +x prisma/seed.sh` to make it executable.
More information in our documentation:
https://pris.ly/d/seeding
```

```
prisma:warn The "ts-node" script in the package.json is not used anymore since version 3.0 and can now be removed.
Error: To configure seeding in your project you need to add a "prisma.seed" property in your package.json with the command to execute it:
```