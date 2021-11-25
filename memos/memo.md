# Links
- [Fullstack app with TypeScript, Next\.js, Prisma & GraphQL](https://www.prisma.io/blog/fullstack-nextjs-graphql-prisma-oklidw1rhw)

- [How to Build a Fullstack App with Next\.js, Prisma, and PostgreSQL – Vercel Docs](https://vercel.com/guides/nextjs-prisma-postgres)

- [How to set up a free PostgreSQL database on Heroku \- DEV Community 👩‍💻👨‍💻](https://dev.to/prisma/how-to-setup-a-free-postgresql-database-on-heroku-1dc1)

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
で`/prisma/schema.prisma`の雛形が生成される。