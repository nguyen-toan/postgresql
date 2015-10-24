Memo on PSQL

* database size
SELECT pg_size_pretty(pg_database_size('DB_NAME'));

* table size
SELECT nspname || '.' || relname AS "relation",
    pg_size_pretty(pg_relation_size(C.oid)) AS "size"
  FROM pg_class C
  LEFT JOIN pg_namespace N ON (N.oid = C.relnamespace)
  WHERE nspname NOT IN ('pg_catalog', 'information_schema')
  ORDER BY pg_relation_size(C.oid) DESC
  LIMIT 20;

* find table name with pattern
SELECT table_name
FROM information_schema.tables
WHERE table_schema = 'public' AND table_name LIKE '%PATTERN%';
