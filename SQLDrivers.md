# SQL database drivers

The database/sql and database/sql/driver packages are designed for using databases from Go and implementing database drivers, respectively.

See the design goals doc:

> http://golang.org/src/pkg/database/sql/doc.txt

# Drivers

Drivers for Go's sql package include:

  * **Couchbase N1QL**: https://github.com/couchbaselabs/go_n1ql
  * **DB2**: https://bitbucket.org/phiggins/db2cli
  * **Firebird SQL**: https://github.com/nakagami/firebirdsql
  * **MS ADODB**: https://github.com/mattn/go-adodb
  * **MS SQL Server** (pure go): https://github.com/denisenkom/go-mssqldb
  * **MySQL**: https://github.com/ziutek/mymysql ` [*] `
  * **MySQL**: https://github.com/go-sql-driver/mysql/ ` [*] `
  * **ODBC**: https://bitbucket.org/miquella/mgodbc
  * **ODBC**: https://github.com/alexbrainman/odbc
  * **Oracle**: https://github.com/mattn/go-oci8
  * **Oracle**: https://github.com/rana/ora
  * **QL**: http://godoc.org/github.com/cznic/ql/driver
  * **Postgres** (pure Go): https://github.com/lib/pq ` [*] `
  * **Postgres** (uses cgo): https://github.com/jbarham/gopgsqldriver
  * **SAP HANA** (pure go): https://github.com/SAP/go-hdb
  * **SQLite**: https://github.com/mattn/go-sqlite3 ` [*] `
  * **SQLite**:  https://github.com/mxk/go-sqlite
  * **Sybase SQL Anywhere**: https://github.com/a-palchikov/sqlago
  * **YQL (Yahoo! Query Language)**: https://github.com/mattn/go-yql

Drivers marked with a ` [*] ` are both included in and pass the compatibility test suite at https://github.com/bradfitz/go-sql-test