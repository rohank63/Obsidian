Notes

SELECT p.proname AS procedure_name,
       a.query AS last_alter_query,
       a.state_change AS last_alter_time
FROM pg_proc p
JOIN pg_stat_activity a ON p.oid = a.objid
WHERE p.proisagg = false  -- Exclude aggregate functions
      AND p.pronamespace <> '11'::regnamespace  -- Exclude system namespaces if needed
      AND p.proisinternal = false  -- Exclude internal procedures if needed
ORDER BY a.state_change DESC
LIMIT 10;  -- Adjust the limit as per your requirement
