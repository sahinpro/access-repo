## 2. Functions

| schema | function_name | arguments | return_type | owner | security_mode | proconfig | anon_execute | authenticated_execute | definition |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| public | is_admin |  | boolean | postgres | SECURITY DEFINER | search_path=public, pg_temp | true | true | CREATE OR REPLACE FUNCTION public.is_admin()<br> RETURNS boolean<br> LANGUAGE sql<br> STABLE SECURITY DEFINER<br> SET search_path TO 'public', 'pg_temp'<br>AS $function$<br>  SELECT EXISTS (<br>    SELECT 1<br>    FROM public.admin_emails a<br>    WHERE lower(a.email) = public.jwt_email()<br>  );<br>$function$<br> |
| public | set_updated_at |  | trigger | postgres | SECURITY INVOKER | search_path=public | true | true | CREATE OR REPLACE FUNCTION public.set_updated_at()<br> RETURNS trigger<br> LANGUAGE plpgsql<br> SET search_path TO 'public'<br>AS $function$<br>BEGIN<br>  NEW.updated_at = now();<br>  RETURN NEW;<br>END;<br>$function$<br> |

## 3. Triggers

| table_schema | table_name | trigger_name | trigger_level | timing | events | enabled | function_return_type | fn_security_mode |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| public | projects | projects_updated_at | ROW | BEFORE | UPDATE | e | trigger | SECURITY INVOKER |
| public | site_settings | site_settings_updated_at | ROW | BEFORE | UPDATE | e | trigger | SECURITY INVOKER |

## 4a. Schema Owners

| schema | owner |
| --- | --- |
| auth | supabase_admin |
| cron | supabase_admin |
| extensions | postgres |
| graphql | supabase_admin |
| graphql_public | supabase_admin |
| net | supabase_admin |
| pgbouncer | pgbouncer |
| public | pg_database_owner |
| realtime | supabase_admin |
| storage | supabase_admin |
| vault | supabase_admin |

## 4b. Function Details

| schema | function_name | arguments | return_type | owner | security_mode | proconfig | anon_execute | authenticated_execute | definer_path_pinned | body_has_truncate | body_has_dynamic_exec | body_has_format |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| auth | email |  | text | supabase_auth_admin | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| auth | jwt |  | jsonb | supabase_auth_admin | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| auth | role |  | text | supabase_auth_admin | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| auth | uid |  | uuid | supabase_auth_admin | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| cron | job_cache_invalidate |  | trigger | supabase_admin | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| cron | schedule | job_name text, schedule text, command text | bigint | supabase_admin | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| cron | schedule | schedule text, command text | bigint | supabase_admin | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| cron | unschedule | job_id bigint | boolean | supabase_admin | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| cron | unschedule | job_name text | boolean | supabase_admin | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | armor | bytea | text | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | armor | bytea, text[], text[] | text | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | crypt | text, text | text | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | dearmor | text | bytea | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | decrypt | bytea, bytea, text | bytea | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | decrypt_iv | bytea, bytea, bytea, text | bytea | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | digest | text, text | bytea | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | digest | bytea, text | bytea | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | encrypt | bytea, bytea, text | bytea | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | encrypt_iv | bytea, bytea, bytea, text | bytea | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | gen_random_bytes | integer | bytea | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | gen_random_uuid |  | uuid | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | gen_salt | text | text | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | gen_salt | text, integer | text | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | grant_pg_cron_access |  | event_trigger | supabase_admin | SECURITY INVOKER | search_path="" | true | true | false | false | false | false |
| extensions | grant_pg_graphql_access |  | event_trigger | supabase_admin | SECURITY INVOKER | search_path="" | true | true | false | false | true | false |
| extensions | grant_pg_net_access |  | event_trigger | supabase_admin | SECURITY INVOKER | search_path="" | true | true | false | false | true | false |
| extensions | hmac | bytea, bytea, text | bytea | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | hmac | text, text, text | bytea | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | pg_stat_statements | showtext boolean, OUT userid oid, OUT dbid oid, OUT toplevel boolean, OUT queryid bigint, OUT query text, OUT plans bigint, OUT total_plan_time double precision, OUT min_plan_time double precision, OUT max_plan_time double precision, OUT mean_plan_time double precision, OUT stddev_plan_time double precision, OUT calls bigint, OUT total_exec_time double precision, OUT min_exec_time double precision, OUT max_exec_time double precision, OUT mean_exec_time double precision, OUT stddev_exec_time double precision, OUT rows bigint, OUT shared_blks_hit bigint, OUT shared_blks_read bigint, OUT shared_blks_dirtied bigint, OUT shared_blks_written bigint, OUT local_blks_hit bigint, OUT local_blks_read bigint, OUT local_blks_dirtied bigint, OUT local_blks_written bigint, OUT temp_blks_read bigint, OUT temp_blks_written bigint, OUT shared_blk_read_time double precision, OUT shared_blk_write_time double precision, OUT local_blk_read_time double precision, OUT local_blk_write_time double precision, OUT temp_blk_read_time double precision, OUT temp_blk_write_time double precision, OUT wal_records bigint, OUT wal_fpi bigint, OUT wal_bytes numeric, OUT jit_functions bigint, OUT jit_generation_time double precision, OUT jit_inlining_count bigint, OUT jit_inlining_time double precision, OUT jit_optimization_count bigint, OUT jit_optimization_time double precision, OUT jit_emission_count bigint, OUT jit_emission_time double precision, OUT jit_deform_count bigint, OUT jit_deform_time double precision, OUT stats_since timestamp with time zone, OUT minmax_stats_since timestamp with time zone | record | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | pg_stat_statements_info | OUT dealloc bigint, OUT stats_reset timestamp with time zone | record | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | pgp_armor_headers | text, OUT key text, OUT value text | record | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | pgp_key_id | bytea | text | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | pgp_pub_decrypt | bytea, bytea | text | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | pgp_pub_decrypt | bytea, bytea, text | text | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | pgp_pub_decrypt | bytea, bytea, text, text | text | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | pgp_pub_decrypt_bytea | bytea, bytea, text, text | bytea | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | pgp_pub_decrypt_bytea | bytea, bytea, text | bytea | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | pgp_pub_decrypt_bytea | bytea, bytea | bytea | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | pgp_pub_encrypt | text, bytea, text | bytea | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | pgp_pub_encrypt | text, bytea | bytea | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | pgp_pub_encrypt_bytea | bytea, bytea, text | bytea | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | pgp_pub_encrypt_bytea | bytea, bytea | bytea | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | pgp_sym_decrypt | bytea, text, text | text | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | pgp_sym_decrypt | bytea, text | text | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | pgp_sym_decrypt_bytea | bytea, text | bytea | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | pgp_sym_decrypt_bytea | bytea, text, text | bytea | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | pgp_sym_encrypt | text, text, text | bytea | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | pgp_sym_encrypt | text, text | bytea | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | pgp_sym_encrypt_bytea | bytea, text | bytea | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | pgp_sym_encrypt_bytea | bytea, text, text | bytea | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | pgrst_ddl_watch |  | event_trigger | supabase_admin | SECURITY INVOKER | search_path="" | true | true | false | false | false | false |
| extensions | pgrst_drop_watch |  | event_trigger | supabase_admin | SECURITY INVOKER | search_path="" | true | true | false | false | false | false |
| extensions | set_graphql_placeholder |  | event_trigger | supabase_admin | SECURITY INVOKER | search_path="" | true | true | false | false | false | false |
| extensions | uuid_generate_v1 |  | uuid | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | uuid_generate_v1mc |  | uuid | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | uuid_generate_v3 | namespace uuid, name text | uuid | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | uuid_generate_v4 |  | uuid | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | uuid_generate_v5 | namespace uuid, name text | uuid | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | uuid_nil |  | uuid | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | uuid_ns_dns |  | uuid | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | uuid_ns_oid |  | uuid | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | uuid_ns_url |  | uuid | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| extensions | uuid_ns_x500 |  | uuid | postgres | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| graphql_public | graphql | "operationName" text, query text, variables jsonb, extensions jsonb | jsonb | supabase_admin | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| net | _await_response | request_id bigint | boolean | supabase_admin | SECURITY INVOKER | (none) | true | true | false | false | true | false |
| net | _encode_url_with_params_array | url text, params_array text[] | text | supabase_admin | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| net | _http_collect_response | request_id bigint, async boolean | net.http_response_result | supabase_admin | SECURITY INVOKER | (none) | true | true | false | false | true | false |
| net | _urlencode_string | string character varying | text | supabase_admin | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| net | check_worker_is_up |  | void | supabase_admin | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| net | http_collect_response | request_id bigint, async boolean | net.http_response_result | supabase_admin | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| net | http_delete | url text, params jsonb, headers jsonb, timeout_milliseconds integer, body jsonb | bigint | supabase_admin | SECURITY INVOKER | (none) | true | true | false | false | true | false |
| net | http_get | url text, params jsonb, headers jsonb, timeout_milliseconds integer | bigint | supabase_admin | SECURITY INVOKER | (none) | true | true | false | false | true | false |
| net | http_post | url text, body jsonb, params jsonb, headers jsonb, timeout_milliseconds integer | bigint | supabase_admin | SECURITY INVOKER | (none) | true | true | false | false | true | false |
| net | wait_until_running |  | void | supabase_admin | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| net | wake |  | void | supabase_admin | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| net | worker_restart |  | boolean | supabase_admin | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| public | is_admin |  | boolean | postgres | SECURITY DEFINER | search_path=public, pg_temp | true | true | true | false | false | false |
| public | set_updated_at |  | trigger | postgres | SECURITY INVOKER | search_path=public | true | true | false | false | false | false |
| realtime | apply_rls | wal jsonb, max_record_bytes integer | realtime.wal_rls | supabase_realtime_admin | SECURITY INVOKER | (none) | true | true | false | false | true | false |
| realtime | authorize | role_name text, topic_name text, claims text, sub text, headers text, read_extensions text[], write_extensions text[], OUT read_allowed boolean[], OUT write_allowed boolean[] | record | supabase_realtime_admin | SECURITY INVOKER | (none) | true | true | false | false | true | false |
| realtime | broadcast_changes | topic_name text, event_name text, operation text, table_name text, table_schema text, new record, old record, level text | void | supabase_realtime_admin | SECURITY INVOKER | (none) | true | true | false | false | true | false |
| realtime | build_prepared_statement_sql | prepared_statement_name text, entity regclass, columns realtime.wal_column[] | text | supabase_realtime_admin | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| realtime | cast | val text, type_ regtype | jsonb | supabase_realtime_admin | SECURITY INVOKER | (none) | true | true | false | false | true | true |
| realtime | check_equality_op | op realtime.equality_op, type_ regtype, val_1 text, val_2 text | boolean | supabase_realtime_admin | SECURITY INVOKER | (none) | true | true | false | false | true | true |
| realtime | check_equality_op | op realtime.equality_op, type_ regtype, val_1 text, val_2 text, negate boolean | boolean | supabase_realtime_admin | SECURITY INVOKER | (none) | true | true | false | false | true | true |
| realtime | is_visible_through_filters | columns realtime.wal_column[], filters realtime.user_defined_filter[] | boolean | supabase_realtime_admin | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| realtime | list_changes | publication name, slot_name name, max_changes integer, max_record_bytes integer | record | supabase_realtime_admin | SECURITY INVOKER | log_min_messages=fatal | true | true | false | false | false | true |
| realtime | list_changes_sync | publication name, slot_name name, max_changes integer, max_record_bytes integer | record | supabase_realtime_admin | SECURITY INVOKER | log_min_messages=fatal | true | true | false | false | false | true |
| realtime | quote_wal2json | entity regclass | text | supabase_realtime_admin | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| realtime | send | payload jsonb, event text, topic text, private boolean | void | supabase_realtime_admin | SECURITY INVOKER | (none) | true | true | false | false | true | true |
| realtime | send_binary | payload bytea, event text, topic text, private boolean | void | supabase_realtime_admin | SECURITY INVOKER | (none) | true | true | false | false | true | true |
| realtime | settled_changes | slot_name name, max_changes integer, VARIADIC opts text[] | record | supabase_realtime_admin | SECURITY INVOKER | (none) | true | true | false | false | true | false |
| realtime | subscription_check_filters |  | trigger | supabase_realtime_admin | SECURITY INVOKER | (none) | true | true | false | false | true | false |
| realtime | to_regrole | role_name text | regrole | supabase_realtime_admin | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| realtime | topic |  | text | supabase_realtime_admin | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| realtime | wal2json_escape_identifier | name text | text | supabase_realtime_admin | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| storage | allow_any_operation | expected_operations text[] | boolean | supabase_storage_admin | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| storage | allow_only_operation | expected_operation text | boolean | supabase_storage_admin | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| storage | can_insert_object | bucketid text, name text, owner uuid, metadata jsonb | void | supabase_storage_admin | SECURITY INVOKER | (none) | true | true | false | false | false | false |
| storage | enforce_bucket_lifecycle_service_role |  | trigger | supabase_storage_admin | SECURITY INVOKER | search_path=pg_catalog | true | true | false | false | false | false |

## 4c. Function Bodies

| schema | function_name | return_type | owner | security_mode | anon_execute | authenticated_execute | body_head |
| --- | --- | --- | --- | --- | --- | --- | --- |
| extensions | grant_pg_graphql_access | event_trigger | supabase_admin | SECURITY INVOKER | true | true | <br>begin<br>    if not exists (<br>        select 1<br>        from pg_catalog.pg_event_trigger_ddl_commands() ev<br>        join pg_catalog.pg_extension e on ev.objid = e.oid<br>        where e.extname = 'pg_graphql'                   |
| extensions | grant_pg_net_access | event_trigger | supabase_admin | SECURITY INVOKER | true | true | <br>BEGIN<br>  IF EXISTS (<br>    SELECT 1<br>    FROM pg_event_trigger_ddl_commands() AS ev<br>    JOIN pg_extension AS ext<br>    ON ev.objid = ext.oid<br>    WHERE ext.extname = 'pg_net'<br>  )<br>  THEN<br>    IF NOT EXISTS (<br>    |
| net | _await_response | boolean | supabase_admin | SECURITY INVOKER | true | true | <br>declare<br>    rec net._http_response;<br>begin<br>    while rec is null loop<br>        select *<br>        into rec<br>        from net._http_response<br>        where id = request_id;<br><br>        if rec is null then<br>        |
| net | _http_collect_response | net.http_response_result | supabase_admin | SECURITY INVOKER | true | true | <br>declare<br>    rec net._http_response;<br>    req_exists boolean;<br>begin<br><br>    if not async then<br>        perform net._await_response(request_id);<br>    end if;<br><br>    select *<br>    into rec<br>    from net._http_res |
| net | http_delete | bigint | supabase_admin | SECURITY INVOKER | true | true | <br>declare<br>    request_id bigint;<br>    params_array text[];<br>begin<br>    select coalesce(array_agg(net._urlencode_string(key) \|\| '=' \|\| net._urlencode_string(value)), '{}')<br>    into params_array<br>    from js            |
| net | http_get | bigint | supabase_admin | SECURITY INVOKER | true | true | <br>declare<br>    request_id bigint;<br>    params_array text[];<br>begin<br>    select coalesce(array_agg(net._urlencode_string(key) \|\| '=' \|\| net._urlencode_string(value)), '{}')<br>    into params_array<br>    from js            |
| net | http_post | bigint | supabase_admin | SECURITY INVOKER | true | true | <br>declare<br>    request_id bigint;<br>    params_array text[];<br>    content_type text;<br>begin<br><br>    -- Exctract the content_type from headers<br>    select<br>        header_value into content_type<br>    from<br>            |
| realtime | apply_rls | realtime.wal_rls | supabase_realtime_admin | SECURITY INVOKER | true | true | <br>declare<br>    -- Regclass of the table e.g. public.notes<br>    entity_ regclass = (quote_ident(wal ->> 'schema') \|\| '.' \|\| quote_ident(wal ->> 'table'))::regclass;<br><br>    -- I, U, D, T: insert, update ...<br>               |
| realtime | authorize | record | supabase_realtime_admin | SECURITY INVOKER | true | true | <br>declare<br>  probe_ids uuid[];<br>  probe_inserted_at timestamp := now() at time zone 'utc';<br>  visible_ids uuid[];<br>  ext text;<br>  allowed boolean;<br>begin<br>  -- The probe inserts are rolled back, but they stil             |
| realtime | broadcast_changes | void | supabase_realtime_admin | SECURITY INVOKER | true | true | <br>DECLARE<br>    -- Declare a variable to hold the JSONB representation of the row<br>    row_data jsonb := '{}'::jsonb;<br>BEGIN<br>    IF level = 'STATEMENT' THEN<br>        RAISE EXCEPTION 'function can only be tr                   |
| realtime | cast | jsonb | supabase_realtime_admin | SECURITY INVOKER | true | true | <br>declare<br>  res jsonb;<br>begin<br>  if type_::text = 'bytea' then<br>    return to_jsonb(val);<br>  end if;<br>  execute format('select to_jsonb(%L::'\|\| type_::text \|\| ')', val) into res;<br>  return res;<br>end<br>            |
| realtime | check_equality_op | boolean | supabase_realtime_admin | SECURITY INVOKER | true | true | <br>/*<br>Casts *val_1* and *val_2* as type *type_* and check the *op* condition for truthiness<br>*/<br>declare<br>    op_symbol text = (<br>        case<br>            when op = 'eq' then '='<br>            when op = 'neq'             |
| realtime | check_equality_op | boolean | supabase_realtime_admin | SECURITY INVOKER | true | true | <br>declare<br>    op_symbol text;<br>    res boolean;<br>begin<br>    -- IS DISTINCT FROM / IS NOT DISTINCT FROM: infix, both sides typed literals<br>    if op = 'isdistinct' then<br>        execute format(<br>            '             |
| realtime | list_changes | record | supabase_realtime_admin | SECURITY INVOKER | true | true | <br>  WITH pub AS (<br>    SELECT<br>      concat_ws(<br>        ',',<br>        CASE WHEN bool_or(pubinsert) THEN 'insert' ELSE NULL END,<br>        CASE WHEN bool_or(pubupdate) THEN 'update' ELSE NULL END,<br>        CA                |
| realtime | list_changes_sync | record | supabase_realtime_admin | SECURITY INVOKER | true | true | <br>  WITH pub AS (<br>    SELECT<br>      concat_ws(<br>        ',',<br>        CASE WHEN bool_or(pubinsert) THEN 'insert' ELSE NULL END,<br>        CASE WHEN bool_or(pubupdate) THEN 'update' ELSE NULL END,<br>        CA                |
| realtime | send | void | supabase_realtime_admin | SECURITY INVOKER | true | true | <br>DECLARE<br>  generated_id uuid;<br>  final_payload jsonb;<br>BEGIN<br>  BEGIN<br>    generated_id := gen_random_uuid();<br><br>    -- Check if payload has an 'id' key, if not, add the generated UUID<br>    IF payload ? 'id'          |
| realtime | send_binary | void | supabase_realtime_admin | SECURITY INVOKER | true | true | <br>DECLARE<br>  generated_id uuid;<br>BEGIN<br>  BEGIN<br>    generated_id := gen_random_uuid();<br><br>    EXECUTE format('SET LOCAL realtime.topic TO %L', topic);<br><br>    INSERT INTO realtime.messages (id, binary_payload,          |
| realtime | settled_changes | record | supabase_realtime_admin | SECURITY INVOKER | true | true | <br>declare<br>  upto pg_lsn;<br>  total bigint;<br>  xids xid[];<br>  starts bigint[];<br>  snapshot pg_snapshot;<br>  running_xids xid[];<br>  xmax_age int;<br>  cut bigint;<br>begin<br>  -- Each statement in a volatile function ta    |
| realtime | subscription_check_filters | trigger | supabase_realtime_admin | SECURITY INVOKER | true | true | <br>declare<br>    col_names text[] = coalesce(<br>            array_agg(a.attname order by a.attnum),<br>            '{}'::text[]<br>        )<br>        from<br>            pg_catalog.pg_attribute a<br>        where<br>                |
| storage | list_objects_with_delimiter | record | supabase_storage_admin | SECURITY INVOKER | true | true | <br>DECLARE<br>    v_peek_name TEXT;<br>    v_current RECORD;<br>    v_common_prefix TEXT;<br><br>    -- Configuration<br>    v_is_asc BOOLEAN;<br>    v_prefix TEXT;<br>    v_start TEXT;<br>    v_start_relative TEXT;<br>    v_upper_b    |
| storage | protect_bucket_control_columns | trigger | supabase_storage_admin | SECURITY INVOKER | true | true | <br>DECLARE<br>  configuration_changed boolean;<br>BEGIN<br>  IF TG_OP = 'INSERT' THEN<br>    IF NEW.lifecycle_configuration IS NOT NULL<br>       OR NEW.lifecycle_configuration_generation IS NOT NULL THEN<br>      IF NOT                |
| storage | search | record | supabase_storage_admin | SECURITY INVOKER | true | true | <br>DECLARE<br>    v_peek_name TEXT;<br>    v_current RECORD;<br>    v_common_prefix TEXT;<br>    v_delimiter CONSTANT TEXT := '/';<br><br>    -- Configuration<br>    v_limit INT;<br>    v_prefix TEXT;<br>    v_prefix_lower TEXT;<br>    |
| storage | search_by_timestamp | record | supabase_storage_admin | SECURITY INVOKER | true | true | <br>DECLARE<br>    v_cursor_op text;<br>    v_query text;<br>    v_prefix text;<br>    v_prefix_pattern text;<br>    v_sort_order text;<br>    v_sort_column text;<br>    v_version_tiebreak text;<br>BEGIN<br>    v_prefix := coalesc       |