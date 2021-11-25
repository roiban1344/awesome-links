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

