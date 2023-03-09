# crispy-winner

这是chatgpt写的一个基于NodeJS 16+和Oracle12C的POC，旨在演示如何使用NodeJS访问和操作Oracle数据库。
首先，需要安装Oracle 12C数据库和NodeJS 16+，并确保已经设置好环境变量。然后，可以通过以下步骤进行POC测试：

1.创建一个新的NodeJS项目，
```
npm init -y

```
并安装以下依赖项：

```
npm install oracledb --save

```

在项目根目录下创建一个config.js文件，包含以下内容：

```
module.exports = {
  user          : process.env.NODE_ORACLEDB_USER || "<your-database-user>",
  password      : process.env.NODE_ORACLEDB_PASSWORD || "<your-database-password>",
  connectString : process.env.NODE_ORACLEDB_CONNECTIONSTRING || "<your-database-connect-string>",
};
```
替换<your-database-user>，<your-database-password>和<your-database-connect-string>为实际值。

3.在项目中创建一个index.js文件，并添加以下内容：

```
const oracledb = require('oracledb');
const config = require('./config.js');

async function run() {
  let connection;

  try {
    connection = await oracledb.getConnection(config);

    const result = await connection.execute(
      `SELECT * FROM <your-table-name>`
    );

    console.dir(result.rows, { depth: null });

  } catch (err) {
    console.error(err);
  } finally {
    if (connection) {
      try {
        await connection.close();
      } catch (err) {
        console.error(err);
      }
    }
  }
}
run();

```
替换<your-table-name>为要查询的实际表名。

4.运行index.js文件：

```
node index.js
```
这将连接到Oracle数据库并执行SELECT语句，然后在控制台上打印查询结果。

通过这个POC，可以看到如何使用NodeJS 16+和Oracle12C进行数据库连接和操作。可以根据实际需要修改代码并添加其他功能。
