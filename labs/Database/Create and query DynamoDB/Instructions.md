# Introduction to Amazon DynamoDB

## Overview

Amazon DynamoDB is a fast and flexible NoSQL database service for applications that need consistent, single-digit millisecond latency at any scale. It is a fully managed database and supports both document and key-value data models. Its flexible data model and reliable performance make it a great fit for mobile, web, gaming, ad-tech, Internet of Things (IoT), and many other applications.

In this lab, I created a table in DynamoDB to store information about a music library, queried the music library, and then deleted the DynamoDB table.

---

## Topics Covered

After completing this lab, I was able to:

- Create an Amazon DynamoDB table
- Enter data into an Amazon DynamoDB table
- Query an Amazon DynamoDB table
- Delete an Amazon DynamoDB table

---

## Introducing the Technologies

### Amazon DynamoDB

DynamoDB is a fully managed NoSQL database service that provides fast and predictable performance with seamless scalability. Unlike traditional relational databases, DynamoDB does not require a fixed schema — each item in a table can have its own unique set of attributes. This flexibility makes it ideal for applications where data structures evolve over time.

### Key DynamoDB Concepts

| Concept | Description |
|---------|-------------|
| **Table** | A collection of data, similar to a table in a relational database |
| **Item** | A single record in a table, similar to a row |
| **Attribute** | A data element within an item, similar to a column |
| **Partition Key** | A required primary key used to distribute data across servers |
| **Sort Key** | An optional secondary key; combined with the partition key, it uniquely identifies each item |

---

## Task 1: Create a New Table

In this task, I created a new table named **Music** in DynamoDB. Each table requires a partition key that is used to partition data across DynamoDB servers. A sort key can also be added — the combination of a partition key and sort key uniquely identifies each item in a DynamoDB table.

1. In the AWS Management Console, choose the **Services** menu. Under **Database**, choose **DynamoDB**.
2. Choose **Create table**.
3. Configure the following settings:
   - **Table name:** `Music`
   - **Partition key:** `Artist` (String)
   - **Sort key:** `Song` (String)
4. Leave all other settings as default and choose **Create table**.

> 📝 **Note:** The table will be created in less than 1 minute. Wait for the Music table status to show **Active** before proceeding.

> ✅ **Task complete:** Successfully created an Amazon DynamoDB table named **Music**.

---

## Task 2: Add Data

In this task, I added data to the Music table. Each record in DynamoDB is called an **item**, and each item is made up of one or more **attributes**. Unlike relational databases, DynamoDB does not enforce a fixed schema — each item can have a different set of attributes.

### Item 1 — Pink Floyd

1. Choose the **Music** table.
2. Choose **Actions** → **Create item**.
3. Enter the following values:

| Attribute Name | Attribute Type | Attribute Value           |
|----------------|----------------|---------------------------|
| Artist         | String         | Pink Floyd                |
| Song           | String         | Money                     |
| Album          | String         | The Dark Side of the Moon |
| Year           | Number         | 1973                      |

4. Choose **Create item**.

### Item 2 — John Lennon

| Attribute Name | Attribute Type | Attribute Value |
|----------------|----------------|-----------------|
| Artist         | String         | John Lennon     |
| Song           | String         | Imagine         |
| Album          | String         | Imagine         |
| Year           | Number         | 1971            |
| Genre          | String         | Soft rock       |

> 📝 **Note:** This item includes an additional `Genre` attribute not present in Item 1, demonstrating that each item can have different attributes without a pre-defined schema.

### Item 3 — Psy

| Attribute Name | Attribute Type | Attribute Value           |
|----------------|----------------|---------------------------|
| Artist         | String         | Psy                       |
| Song           | String         | Gangnam Style             |
| Album          | String         | Psy 6 (Six Rules), Part 1 |
| Year           | Number         | 2011                      |
| LengthSeconds  | Number         | 219                       |

> 📝 **Note:** This item introduces a `LengthSeconds` attribute, further demonstrating the schema flexibility of a NoSQL database.

> ✅ **Task complete:** Successfully entered data into the Amazon DynamoDB table.

---

## Task 3: Modify an Existing Item

In this task, I corrected an error in the data by updating the **Year** attribute for the Psy item.

1. In the DynamoDB dashboard, choose **Explore Items**.
2. Select the **Music** table.
3. Choose **Psy**.
4. Update the **Year** value from `2011` to `2012`.
5. Choose **Save changes**.

> ✅ **Task complete:** Successfully modified an existing item in the DynamoDB table.

---

## Task 4: Query the Table

In this task, I queried the Music table using two methods: **Query** and **Scan**.

### Method 1: Query

A **query** finds items based on the partition key and optionally the sort key. It is fully indexed, making it very fast and efficient.

1. Expand **Scan/Query items** and choose **Query**.
2. Enter the following values:
   - **Artist (Partition key):** `Psy`
   - **Song (Sort key):** `Gangnam Style`
3. Choose **Run**.

The matching item appears immediately, demonstrating the efficiency of a query operation.

### Method 2: Scan

A **scan** reads every item in the table and then filters results. It is less efficient than a query and can be slow on large tables.

1. Choose **Scan**.
2. Expand **Filters** and enter the following values:
   - **Attribute name:** `Year`
   - **Type:** `Number`
   - **Value:** `1971`
3. Choose **Run**.

Only the song released in 1971 (John Lennon — *Imagine*) is returned.

> 💭 **Consider:** For large production tables, always prefer a **Query** over a **Scan** where possible to minimise read costs and latency.

> ✅ **Task complete:** Successfully queried the Amazon DynamoDB table using both Query and Scan operations.

---

## Task 5: Delete the Table

In this task, I deleted the Music table. Deleting a table also permanently removes all data stored within it.

1. In the DynamoDB dashboard, under **Tables**, choose **Update settings**.
2. Select the **Music** table.
3. Choose **Actions** → **Delete table**.
4. In the confirmation panel, enter `delete` and choose **Delete table**.

> ⚠️ **Caution:** Deleting a DynamoDB table is permanent and cannot be undone. All items stored in the table will be lost.

> ✅ **Task complete:** Successfully deleted the Amazon DynamoDB table.

---

## Conclusion

🎉 **Congratulations!** You have now successfully:

- ✅ Created an Amazon DynamoDB table
- ✅ Entered data into an Amazon DynamoDB table
- ✅ Queried an Amazon DynamoDB table
- ✅ Deleted an Amazon DynamoDB table

---

## Additional Resources

- [Amazon DynamoDB Documentation](https://docs.aws.amazon.com/dynamodb/)
- [Core Components of Amazon DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/HowItWorks.CoreComponents.html)
- [DynamoDB Query vs Scan](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Query.html)
- [AWS Training and Certification](https://aws.amazon.com/training/)
