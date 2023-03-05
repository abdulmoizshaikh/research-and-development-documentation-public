# Prisma

Useful Commands:

## Prisma Studio - A Visual Interface for Your Database

![studio_microphone](https://github.githubassets.com/images/icons/emoji/unicode/1f399.png) The easiest way to explore and manipulate your data in all of your Prisma projects.

```bash showLineNumbers
npx prisma studio
```

https://github.com/prisma/studio

`prisma:warn The prisma introspect command is deprecated. Please use prisma db pull instead.`

https://www.prisma.io/blog/prisma-studio-3rtf78dg99fe

Prisma 2 Impressions with NestJS | Next-gen Node.JS ORM?!

https://www.youtube.com/watch?v=Aq1U_Ku8Jig&t=1s&ab_channel=MariusEspejo

## Prisma with Nestjs

**Getting started**

https://docs.nestjs.com/recipes/prisma

### Relations

## Types of relations

There are three different types (or [cardinalities](<https://en.wikipedia.org/wiki/Cardinality_(data_modeling)>)) of relations in Prisma:

- [One-to-one](https://www.prisma.io/docs/concepts/components/prisma-schema/relations/one-to-one-relations) (also called 1-1-relation)
- [One-to-many](https://www.prisma.io/docs/concepts/components/prisma-schema/relations/one-to-many-relations) (also called 1-n-relation)
- [Many-to-many](https://www.prisma.io/docs/concepts/components/prisma-schema/relations/many-to-many-relations) (also called m-n-relation)

https://www.prisma.io/docs/concepts/components/prisma-schema/relations

**Prisma**

https://docs.nestjs.com/recipes/prisma

https://www.prisma.io/docs/getting-started/quickstart

prisma vs typeorm

https://www.prisma.io/docs/concepts/more/comparisons/prisma-and-typeorm#type-safety

## Middleware

### Track all modifications to a PostgreSQL table

but we can do through $use middleware in prisma which is recommended

https://www.prisma.io/docs/concepts/components/prisma-client/middleware?query=logger&page=1

https://dba.stackexchange.com/questions/233735/track-all-modifications-to-a-postgresql-table

### How to add a prisma middleware in different file

```jsx showLineNumbers
// File: prisma.ts

import { PrismaClient, Prisma } from "@prisma/client";
import * as middleware from "./prismaMiddleware";

const prisma: PrismaClient = new PrismaClient();

prisma.$use(middleware.Encrypt);

// File: prismaMiddleware.ts
import { Prisma } from "@prisma/client";
import bcrypt from "bcryptjs";
export const Encrypt: Prisma.Middleware = async (
  params: Prisma.MiddlewareParams,
  next
) => {
  if (params.action == "create" && params.model == "User") {
    let user = params.args.data;
    let salt = bcrypt.genSaltSync(10);
    let hash = bcrypt.hashSync(user.password, salt);
    user.password = hash;
  }
  return await next(params);
};
```

https://stackoverflow.com/questions/68453660/how-to-add-a-prisma-middleware-in-different-file

### Where is the best place to put prisma middleware on NestJs?

https://stackoverflow.com/questions/69581717/where-is-the-beest-place-to-put-prisma-middleware-on-nestjs

### Command to detech change in your schema.prisma models and automatically generate migration for that change

```bash showLineNumbers
npx prisma migrate dev
```

**Searching functionality work same as LIKE keyword in SQL in prisma**
search by name query in prisma
like query in prisma

Solution:

Use `contains` and `mode` property for search string in case sensitive

```jsx showLineNumbers
where: {
          category2: {
            contains: category,
            mode: 'insensitive',
          },
        },
```

https://www.prisma.io/docs/reference/api-reference/prisma-client-reference#string_contains

https://www.prisma.io/docs/reference/api-reference/prisma-client-reference#mode

https://www.prisma.io/docs/reference/api-reference/prisma-client-reference#search

**how to add multiple or in prisma**

Sol:
Great call, except

```sql
AND: [ { OR: [ { key: value } ] }, { OR: [ { key: value } ]
```

```jsx
const rate = await prisma.contractRate.findFirst({
  where: {
    hefazatProductTypeId: hefazatProductType.name,
    revenueModel: RevenueModel.B2B2C,
    partnerId: context.user.partners[0].partnerId,
    AND: [
      {
        OR: [
          {
            categoryGroup: pm.categoryGroup,
          },
          {
            categoryGroup: CategoryGroup.ANY_,
          },
        ],
      },
      {
        OR: [
          {
            province: contract.customer.province,
          },
          {
            province: "ANY_",
          },
        ],
      },
    ],
  },
});
```

https://github.com/prisma/prisma-client-js/issues/406

## Migrations in Prisma

**How to check migrations table in db for prisma migrations**

where to delete migration transaction in pgadmin

where is the migration table in postgresql

invalid input value for enum postgres force update

Ans:

```sql showLineNumbers
SELECT * FROM public._prisma_migrations
ORDER BY "finished_at" desc
```

and delete folder for migration in prisma-> migrations folder to revert migration

If you want to update enum types make sure you first add new enum type and then update query run on table and replace records that are aleardy created with enum types that needs to be deleted and then create new migration with delete enum type it will work

my target was to change enum type name from `Completed` to `Approved` in hefazat postgresql db with prisma ORM migration and I did it by these steps

e.g

```sql showLineNumbers
SELECT * FROM public."Claim"
WHERE "state"='Completed'

UPDATE public."Claim"
SET "state"='Approved'
WHERE "state"='Completed'

SELECT * FROM public."Claim"
WHERE "state"='Approved'

```

### Using Prisma's Group By Feature

<iframe width="100%" height="494" src="https://www.youtube.com/embed/BdlCPdPaorY" title="Using Prisma's Group By Feature" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen="true"></iframe>

https://www.youtube.com/watch?v=BdlCPdPaorY&ab_channel=Prisma

**It's Prisma Time - Aggregate and GroupBy**

tags:
distinct in where clause prisma
DISTINCT count in prisma

```jsx showLineNumbers
const commentsGroupByPost = await prisma.comment.groupBy({
  by: ["postId"],
  _count: {
    authorId: true,
    _all: true,
  },
  orderBy: {
    _count: {
      authorId: "desc",
    },
  },
  having: {
    authorId: {
      _count: {
        gt: 1,
      },
    },
  },
});
```

Equivalent Raw query

```sql showLineNumbers
SELECT
q."mobile",q."customerCnic"
FROM public."ContractQuote" q
LEFT JOIN "Contract" cont on cont."quoteId" = q."contractQuoteId"
WHERE (cont."queue"='DataCompleted' OR cont."queue"='ContractDone')
AND q."mobile"='+923222222223'
group by q."mobile",q."customerCnic"

```

https://dev.to/this-is-learning/its-prisma-time-aggregate-and-groupby-36a7

**composite unique in prisma schema**

Prisma - How to define compound unique constraint with fields in multiple models?

```jsx showLineNumbers
  @@unique([serialNo, hefazatProductTypeId])
```

## Index in prisma

indexing in prisma postgresql

```jsx showLineNumbers
  @@unique([serialNo, hefazatProductTypeId])
```

e.g

> worked on it in hefazat backend project

```jsx showLineNumbers

model B2BSerialNoMap {
  B2BSerialNoMapId     Int                @id @default(autoincrement())
  serialNo             String
  revenueModel         RevenueModel
  consumed             Boolean            @default(false)
  hefazatProductTypeId String
  hefazatProductType   HefazatProductType @relation(fields: [hefazatProductTypeId], references: [name])
  partnerId            Int
  partner              Partner            @relation(fields: [partnerId], references: [partnerId])
  createdAt            DateTime           @default(now())
  createdBy            String             @default("SystemUser")
  updatedAt            DateTime           @updatedAt
  updatedBy            String             @default("SystemUser")

  @@unique([serialNo, hefazatProductTypeId])
  @@index([serialNo])
}

```

https://www.prisma.io/docs/concepts/components/prisma-schema/indexes

https://stackoverflow.com/questions/67226972/prisma-how-to-define-compound-unique-constraint-with-fields-in-multiple-models

https://www.prisma.io/docs/concepts/components/prisma-client/composite-types

https://www.youtube.com/watch?v=ot8dwJ8x850&ab_channel=OnlineStudyForCS

https://www.prisma.io/blog/improving-query-performance-using-indexes-2-MyoiJNMFTsfq

https://www.prisma.io/blog/improving-query-performance-using-indexes-3-kduk351qv1

### How to import data into pgadmin from csv file

https://youtu.be/ot8dwJ8x850?t=170

### How to check cost of query in postgresql

by using `Explain` keywork in start of query

it will give details about count of rows and query execution time etc

https://youtu.be/ot8dwJ8x850?t=441

## Bug fixing

**Transaction API error: Transaction already closed: Transaction is no longer valid. Last state: 'Expired' P2028**
#13713

Transaction already closed: Transaction is no longer valid.

Answer:

I was using forEach loop inside transaction API of prisma
Just replaced forEach Loop with for loop and issue fixed

https://github.com/prisma/prisma/issues/13713

## Joins in prisma

you can only use join in prisma using raq query as described in official documentation

https://www.prisma.io/dataguide/postgresql/reading-and-querying-data/joining-tables#inner-join
