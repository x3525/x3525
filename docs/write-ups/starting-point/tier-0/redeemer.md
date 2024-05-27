---
glightbox: true
---

# Redeemer

!!! info "Target IP Address"

    10.129.99.162

Hedef makine için Nmap taraması gerçekleştir:

```bash
sudo nmap 10.129.99.162 -T5 -Pn -p-
```

```text title="Output" hl_lines="6"
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-01-21 23:07 +03
Nmap scan report for 10.129.99.162
Host is up (0.14s latency).
Not shown: 62503 closed tcp ports (reset), 3031 filtered tcp ports (no-response)
PORT     STATE SERVICE
6379/tcp open  redis

Nmap done: 1 IP address (1 host up) scanned in 782.02 seconds
```

Redis sunucusuna bağlan ve bağlandıktan sonra `info` komutunu çalıştır:

```bash
redis-cli -h 10.129.99.162
```

```text title="Output" hl_lines="138-139"
# Server
redis_version:5.0.7
redis_git_sha1:00000000
redis_git_dirty:0
redis_build_id:66bd629f924ac924
redis_mode:standalone
os:Linux 5.4.0-77-generic x86_64
arch_bits:64
multiplexing_api:epoll
atomicvar_api:atomic-builtin
gcc_version:9.3.0
process_id:754
run_id:7e9cb9c1917cb26e19cd6af51b797768806b56e3
tcp_port:6379
uptime_in_seconds:961
uptime_in_days:0
hz:10
configured_hz:10
lru_clock:11369735
executable:/usr/bin/redis-server
config_file:/etc/redis/redis.conf

# Clients
connected_clients:1
client_recent_max_input_buffer:2
client_recent_max_output_buffer:0
blocked_clients:0

# Memory
used_memory:859624
used_memory_human:839.48K
used_memory_rss:5865472
used_memory_rss_human:5.59M
used_memory_peak:859624
used_memory_peak_human:839.48K
used_memory_peak_perc:100.12%
used_memory_overhead:847166
used_memory_startup:797248
used_memory_dataset:12458
used_memory_dataset_perc:19.97%
allocator_allocated:1568600
allocator_active:1892352
allocator_resident:9101312
total_system_memory:2084024320
total_system_memory_human:1.94G
used_memory_lua:41984
used_memory_lua_human:41.00K
used_memory_scripts:0
used_memory_scripts_human:0B
number_of_cached_scripts:0
maxmemory:0
maxmemory_human:0B
maxmemory_policy:noeviction
allocator_frag_ratio:1.21
allocator_frag_bytes:323752
allocator_rss_ratio:4.81
allocator_rss_bytes:7208960
rss_overhead_ratio:0.64
rss_overhead_bytes:-3235840
mem_fragmentation_ratio:7.17
mem_fragmentation_bytes:5047856
mem_not_counted_for_evict:0
mem_replication_backlog:0
mem_clients_slaves:0
mem_clients_normal:49694
mem_aof_buffer:0
mem_allocator:jemalloc-5.2.1
active_defrag_running:0
lazyfree_pending_objects:0

# Persistence
loading:0
rdb_changes_since_last_save:0
rdb_bgsave_in_progress:0
rdb_last_save_time:1705868491
rdb_last_bgsave_status:ok
rdb_last_bgsave_time_sec:0
rdb_current_bgsave_time_sec:-1
rdb_last_cow_size:417792
aof_enabled:0
aof_rewrite_in_progress:0
aof_rewrite_scheduled:0
aof_last_rewrite_time_sec:-1
aof_current_rewrite_time_sec:-1
aof_last_bgrewrite_status:ok
aof_last_write_status:ok
aof_last_cow_size:0

# Stats
total_connections_received:5
total_commands_processed:6
instantaneous_ops_per_sec:0
total_net_input_bytes:306
total_net_output_bytes:11572
instantaneous_input_kbps:0.00
instantaneous_output_kbps:0.00
rejected_connections:0
sync_full:0
sync_partial_ok:0
sync_partial_err:0
expired_keys:0
expired_stale_perc:0.00
expired_time_cap_reached_count:0
evicted_keys:0
keyspace_hits:0
keyspace_misses:0
pubsub_channels:0
pubsub_patterns:0
latest_fork_usec:273
migrate_cached_sockets:0
slave_expires_tracked_keys:0
active_defrag_hits:0
active_defrag_misses:0
active_defrag_key_hits:0
active_defrag_key_misses:0

# Replication
role:master
connected_slaves:0
master_replid:1ceef55eed866f10a69247601d8918b0009e2c97
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:0
second_repl_offset:-1
repl_backlog_active:0
repl_backlog_size:1048576
repl_backlog_first_byte_offset:0
repl_backlog_histlen:0

# CPU
used_cpu_sys:0.487503
used_cpu_user:0.492622
used_cpu_sys_children:0.000000
used_cpu_user_children:0.000914

# Cluster
cluster_enabled:0

# Keyspace
db0:keys=4,expires=0,avg_ttl=0
```

Veri tabanını seç (index 0 için):

```text
select 0
```

Aşağıdaki komut ile bayrağı ele geçir:

```text
get flag
```
