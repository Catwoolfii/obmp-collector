# Using Logstash with OpenBMP

## Installing Logstash
[Visit download page](https://www.elastic.co/downloads/logstash)

## Starting logstash
Go to your logstash installation location, and run

`logstash -f openbmp-logstash.conf`

## Expanding
With logstash, you can easily get a variety of [possible outputs](https://www.elastic.co/guide/en/logstash/current/output-plugins.html). Here we provide elasticsearch output configuration with openBMP kafka input. To use other outputs or add custom data processing, add other plugins to **filter** section and **output** section. Note that **plugins execute in the order they appear**.

## Logstash config
```
input {
    kafka {
        codec => plain
        bootstrap_servers => "localhost:9092"
        topics => "openbmp.parsed.collector"
        group_id => "default"
        client_id => "cra-logstash"
        auto_offset_reset => "earliest"
        isolation_level => "read_committed"
        connections_max_idle_ms => 60000
        request_timeout_ms => 30000
        #security_protocol => "SASL_PLAINTEXT"
        #sasl_mechanism => "SCRAM-SHA-256"
        #sasl_jaas_config => "org.apache.kafka.common.security.scram.ScramLoginModule required username='<user>' password='<passwd>';"
        add_field => { "[@metadata][TOPIC]" => "openbmp.parsed.collector" }
    }
    kafka {
        codec => plain
        bootstrap_servers => "localhost:9092"
        topics => "openbmp.parsed.router"
        group_id => "default"
        client_id => "cra-logstash"
        auto_offset_reset => "earliest"
        isolation_level => "read_committed"
        connections_max_idle_ms => 60000
        request_timeout_ms => 30000
        #security_protocol => "SASL_PLAINTEXT"
        #sasl_mechanism => "SCRAM-SHA-256"
        #sasl_jaas_config => "org.apache.kafka.common.security.scram.ScramLoginModule required username='<user>' password='<passwd>';"
        add_field => { "[@metadata][TOPIC]" => "openbmp.parsed.router" }
    }
    kafka {
        codec => plain
        bootstrap_servers => "localhost:9092"
        topics => "openbmp.parsed.peer"
        group_id => "default"
        client_id => "cra-logstash"
        auto_offset_reset => "earliest"
        isolation_level => "read_committed"
        connections_max_idle_ms => 60000
        request_timeout_ms => 30000
        #security_protocol => "SASL_PLAINTEXT"
        #sasl_mechanism => "SCRAM-SHA-256"
        #sasl_jaas_config => "org.apache.kafka.common.security.scram.ScramLoginModule required username='<user>' password='<passwd>';"
        add_field => { "[@metadata][TOPIC]" => "openbmp.parsed.peer" }
    }
    kafka {
        codec => plain
        bootstrap_servers => "localhost:9092"
        topics => "openbmp.parsed.bmp_stat"
        group_id => "default"
        client_id => "cra-logstash"
        auto_offset_reset => "earliest"
        isolation_level => "read_committed"
        connections_max_idle_ms => 60000
        request_timeout_ms => 30000
        #security_protocol => "SASL_PLAINTEXT"
        #sasl_mechanism => "SCRAM-SHA-256"
        #sasl_jaas_config => "org.apache.kafka.common.security.scram.ScramLoginModule required username='<user>' password='<passwd>';"
        add_field => { "[@metadata][TOPIC]" => "openbmp.parsed.bmp_stat" }
    }
    kafka {
        codec => plain
        bootstrap_servers => "localhost:9092"
        topics => "openbmp.parsed.base_attribute"
        group_id => "default"
        client_id => "cra-logstash"
        auto_offset_reset => "earliest"
        isolation_level => "read_committed"
        connections_max_idle_ms => 60000
        request_timeout_ms => 30000
        #security_protocol => "SASL_PLAINTEXT"
        #sasl_mechanism => "SCRAM-SHA-256"
        #sasl_jaas_config => "org.apache.kafka.common.security.scram.ScramLoginModule required username='<user>' password='<passwd>';"
        add_field => { "[@metadata][TOPIC]" => "openbmp.parsed.base_attribute" }
    }
    kafka {
        codec => plain
        bootstrap_servers => "localhost:9092"
        topics => "openbmp.parsed.unicast_prefix"
        group_id => "default"
        client_id => "cra-logstash"
        auto_offset_reset => "earliest"
        isolation_level => "read_committed"
        connections_max_idle_ms => 60000
        request_timeout_ms => 30000
        #security_protocol => "SASL_PLAINTEXT"
        #sasl_mechanism => "SCRAM-SHA-256"
        #sasl_jaas_config => "org.apache.kafka.common.security.scram.ScramLoginModule required username='<user>' password='<passwd>';"
        add_field => { "[@metadata][TOPIC]" => "openbmp.parsed.unicast_prefix" }
    }
    kafka {
        codec => plain
        bootstrap_servers => "localhost:9092"
        topics => "openbmp.parsed.ls_node"
        group_id => "default"
        client_id => "cra-logstash"
        auto_offset_reset => "earliest"
        isolation_level => "read_committed"
       connections_max_idle_ms => 60000
        request_timeout_ms => 30000
        #security_protocol => "SASL_PLAINTEXT"
        #sasl_mechanism => "SCRAM-SHA-256"
        #sasl_jaas_config => "org.apache.kafka.common.security.scram.ScramLoginModule required username='<user>' password='<passwd>';"
        add_field => { "[@metadata][TOPIC]" => "openbmp.parsed.ls_node" }
    }
    kafka {
        codec => plain
        bootstrap_servers => "localhost:9092"
        topics => "openbmp.parsed.ls_link"
        group_id => "default"
        client_id => "cra-logstash"
        auto_offset_reset => "earliest"
        isolation_level => "read_committed"
        connections_max_idle_ms => 60000
        request_timeout_ms => 30000
        #security_protocol => "SASL_PLAINTEXT"
        #sasl_mechanism => "SCRAM-SHA-256"
        #sasl_jaas_config => "org.apache.kafka.common.security.scram.ScramLoginModule required username='<user>' password='<passwd>';"
        add_field => { "[@metadata][TOPIC]" => "openbmp.parsed.ls_link" }
    }
    kafka {
        codec => plain
        bootstrap_servers => "localhost:9092"
        topics => "openbmp.parsed.ls_prefix"
        group_id => "default"
        client_id => "cra-logstash"
        auto_offset_reset => "earliest"
        isolation_level => "read_committed"
        connections_max_idle_ms => 60000
        request_timeout_ms => 30000
        #security_protocol => "SASL_PLAINTEXT"
        #sasl_mechanism => "SCRAM-SHA-256"
        #sasl_jaas_config => "org.apache.kafka.common.security.scram.ScramLoginModule required username='<user>' password='<passwd>';"
        add_field => { "[@metadata][TOPIC]" => "openbmp.parsed.ls_prefix" }
    }
    kafka {
        codec => plain
        bootstrap_servers => "localhost:9092"
        topics => "openbmp.parsed.l3vpn"
        group_id => "default"
        client_id => "cra-logstash"
        auto_offset_reset => "earliest"
        isolation_level => "read_committed"
        connections_max_idle_ms => 60000
        request_timeout_ms => 30000
        #security_protocol => "SASL_PLAINTEXT"
        #sasl_mechanism => "SCRAM-SHA-256"
        #sasl_jaas_config => "org.apache.kafka.common.security.scram.ScramLoginModule required username='<user>' password='<passwd>';"
        add_field => { "[@metadata][TOPIC]" => "openbmp.parsed.l3vpn" }
    }
#    kafka {
#        codec => plain
#        bootstrap_servers => "localhost:9092"
#        topics => "openbmp.parsed.evpn"
#        group_id => "default"
#        client_id => "cra-logstash"
#        auto_offset_reset => "earliest"
#        isolation_level => "read_committed"
#        connections_max_idle_ms => 60000
#        request_timeout_ms => 30000
#        #security_protocol => "SASL_PLAINTEXT"
#        #sasl_mechanism => "SCRAM-SHA-256"
#        #sasl_jaas_config => "org.apache.kafka.common.security.scram.ScramLoginModule required username='<user>' password='<passwd>';"
#        add_field => { "[@metadata][TOPIC]" => "openbmp.parsed.evpn" }
#    }
}

filter {
    mutate {
        split => ["message", "

"]
        add_field => { "HEADER" => "%{[message][1]}" }
        remove_field => ["message"]
    }
    if [@metadata][TOPIC] == "openbmp.parsed.collector" {
        csv {
            source => ["HEADER"]
            #need to set the value of "separator" to the actual tab character and not "\t"!
            separator => "	"
            columns => ["state", "sequence", "admin_id", "hash_id", "routers", "router_count", "timestamp"]
            remove_field => ["HEADER", "column7", "@version", "@timestamp", "sequence"]
            convert => {
                "router_count" => "integer"
            }
        }
#        mutate {
#            gsub => [ "state", "heartbeat", "up", "state", "started", "up",
#                      "state",  "change", "up", "state", "stopped", "down" ]
#        }
        if [state] in [ "heartbeat", "started", "change" ] {
            mutate {
                update => { "state" => "up" }
            }
        }
        else if [state] == "stopped" {
            mutate {
                update => { "state" => "down" }
            }
        }
    }
    if [@metadata][TOPIC] == "openbmp.parsed.router" {
        csv {
            source => ["HEADER"]
            #need to set the value of "separator" to the actual tab character and not "\t"!
            separator => "	"
            columns => ["state", "sequence", "name", "hash_id", "ip_address", "description", "term_code",
                        "term_reason_text", "init_data", "term_data", "timestamp", "bgp_id"]
            remove_field => ["HEADER", "column12", "@version", "@timestamp", "sequence"]
            convert => {
                "term_code" => "integer"
            }
        }
#        mutate {
#            gsub => [ "state", "first", "up", "state", "init", "up",
#                      "state", "term", "down" ]
#        }
        if [state] in [ "first", "init" ] {
            mutate {
                update => { "state" => "up" }
            }
        }
        else if [state] == "term" {
            mutate {
                update => { "state" => "down" }
            }
        }
    }
    if [@metadata][TOPIC] == "openbmp.parsed.peer" {
        csv {
            source => ["HEADER"]
            #need to set the value of "separator" to the actual tab character and not "\t"!
            separator => "	"
            columns => ["state", "sequence", "hash_id", "router_hash_id", "name", "remote_bgp_id", "router_ip",
                        "timestamp", "remote_asn", "remote_ip", "peer_rd", "remote_port", "local_asn",
                        "local_ip", "local_port", "local_bgp_id", "info_data", "sent_capabilities",
                        "recv_capabilities", "remote_holddown", "adv_holddown", "bmp_reason", "bgp_error_code",
                        "bgp_error_subcode", "error_text", "is_l3vpn", "is_pre_policy", "is_ipv4", "is_loc_rib",
                        "is_loc_rib_filtered", "table_name"]
            remove_field => ["HEADER", "column31", "@version", "@timestamp", "sequence", "router_ip",
                             "info_data"]
            convert => {
                "is_ipv4" => "integer"
                "remote_asn" => "integer"
                "is_l3vpn" => "integer"
                "is_pre_policy" => "integer"
                "local_port" => "integer"
                "adv_holddown" => "integer"
                "local_asn" => "integer"
                "remote_port" => "integer"
                "remote_holddown" => "integer"
                "bmp_reason" => "integer"
                "bgp_err_code" => "integer"
                "bgp_err_subcode" => "integer"
                "is_loc_rib" => "integer"
                "is_loc_rib_filtered" => "integer"
            }
        }
        mutate {
            gsub => [ "state", "first", "up" ]
        }
    }
    if [@metadata][TOPIC] == "openbmp.parsed.bmp_stat" {
        csv {
            source => ["HEADER"]
            #need to set the value of "separator" to the actual tab character and not "\t"!
            separator => "	"
            columns => ["action", "sequence", "router_hash_id", "router_ip", "peer_hash_id", "peer_ip", "peer_asn",
                        "timestamp", "prefixes_rejected", "known_dup_prefixes", "known_dup_withdraws",
                        "invalid_cluster_list", "invalid_as_path", "invalid_originator_id", "invalid_as_confed",
                        "prefixes_pre_policy", "prefixes_post_policy"]
            remove_field => ["HEADER", "column17", "@version", "@timestamp", "action", "sequence", "router_hash_id",
                             "router_ip", "peer_ip", "peer_asn"]
            convert => {
                "prefixes_rejected" => "integer"
                "known_dup_prefixes" => "integer"
                "known_dup_withdraws" => "integer"
                "invalid_cluster_list" => "integer"
                "invalid_as_path" => "integer"
                "invalid_originagtor_id" => "integer"
                "invalid_as_confed" => "integer"
                "prefixes_pre_policy" => "integer"
                "prefixes_post_policy" => "integer"
            }
        }
    }
    if [@metadata][TOPIC] == "openbmp.parsed.base_attribute" {
        csv {
            source => ["HEADER"]
            #need to set the value of "separator" to the actual tab character and not "\t"!
            separator => "	"
            columns => ["action", "sequence", "hash_id", "router_hash_id", "router_ip", "peer_hash_id", "peer_ip",
                        "peer_asn", "timestamp", "origin", "as_path", "as_path_count", "origin_as", "next_hop",
                        "med", "local_pref", "aggregator", "community_list", "ext_community_list", "cluster_list",
                        "is_atomic_agg", "is_next_hop_ipv4", "originator_id", "large_community_list"]
            remove_field => ["HEADER", "column24", "@version", "@timestamp", "action", "sequence", "router_hash_id",
                             "router_ip", "peer_ip", "peer_asn"]
            convert => {
                "as_path_count" => "integer"
                "origin_as" => "integer"
                "med" => "integer"
                "local_pref" => "integer"
                "is_atomic_agg" => "integer"
                "is_next_hop_ipv4" => "integer"
            }
        }
        if ! [as_path] {
            mutate {
                update => { "as_path" => "" }
            }
        }
        mutate {
           split => [ "as_path", " " ]
        }
        mutate {
           convert => { "as_path" => "integer" }
        }
        if ! [community_list] {
            mutate {
                update => { "community_list" => "" }
            }
        }
        mutate {
           split => [ "community_list", " " ]
        }
        if ! [ext_community_list] {
            mutate {
                update => { "ext_community_list" => "" }
            }
        }
        mutate {
           split => [ "ext_community_list", " " ]
        }
        if ! [cluster_list] {
            mutate {
                update => { "cluster_list" => "" }
            }
        }
        mutate {
           split => [ "cluster_list", " " ]
        }
        if ! [large_community_list] {
            mutate {
                update => { "large_community_list" => "" }
            }
        }
        mutate {
           split => [ "large_community_list", " " ]
        }
    }
    if [@metadata][TOPIC] == "openbmp.parsed.unicast_prefix" {
        csv {
            source => ["HEADER"]
            #need to set the value of "separator" to the actual tab character and not "\t"!
            separator => "	"
            columns => ["iswithdrawn", "sequence", "hash_id", "router_hash_id", "router_ip", "base_attr_hash_id", "peer_hash_id",
                        "peer_ip", "peer_asn", "timestamp", "prefix", "prefix_len", "is_ipv4", "origin", "as_path",
                        "as_path_count", "origin_as", "next_hop", "med", "local_pref", "aggregator", "community_list",
                        "ext_community_list", "cluster_list", "is_atomic_agg", "is_next_hop_ipv4", "originator_id",
                        "path_id", "labels", "is_pre_policy", "is_adj_in", "large_community_list"]
            remove_field => ["HEADER", "column32", "@version", "@timestamp", "sequence", "router_hash_id", "router_ip",
                             "peer_ip", "peer_asn", "origin", "as_path", "as_path_count", "next_hop", "med",
                             "cluster_list", "is_atomic_agg", "is_next_hop_ipv4", "originator_id", "large_community_list"]
            convert => {
                "is_ipv4" => "integer"
                "origin_as" => "integer"
                "prefix_len" => "integer"
                "path_id" => "integer"
                "is_pre_policy" => "integer"
                "is_adj_in" => "integer"
            }
        }
        mutate {
            update => { "prefix" => "%{[prefix]}/%{[prefix_len]}" }
        }
        if [iswithdrawn] == "add" {
            mutate {
                update => { "iswithdrawn" => "0" }
            }
        }
        else if [iswithdrawn] == "del" {
            mutate {
                update => { "iswithdrawn" => "1" }
            }
        }
        mutate {
            convert => {  "iswithdrawn" => "integer" }
        }
    }
    if [@metadata][TOPIC] == "openbmp.parsed.ls_node" {
        csv {
            source => ["HEADER"]
            #need to set the value of "separator" to the actual tab character and not "\t"!
            separator => "	"
            columns => ["iswithdrawn", "sequence", "hash_id", "base_attr_hash_id", "router_hash_id", "router_ip", "peer_hash_id",
                        "peer_ip", "peer_asn", "timestamp", "igp_router_id", "router_id", "routing_id", "ls_id", "mt_id",
                        "ospf_area_id", "isis_area_id", "protocol", "flags", "as_path", "local_pref", "med", "next_hop",
                        "name", "is_pre_policy", "is_adj_in", "sr_capabilities"]
           remove_field => ["HEADER", "column27", "@version", "@timestamp", "router_hash_id", "router_ip",
                            "peer_ip", "routing_id", "as_path", "local_pref", "med", "next_hop",
                            "is_pre_policy", "is_adj_in"]
            convert => {
                "sequence" => "integer"
                "peer_asn" => "integer"
                "ls_id" => "integer"
            }
        }
        if [iswithdrawn] == "add" {
            mutate {
                update => { "iswithdrawn" => "0" }
            }
        }
        else if [iswithdrawn] == "del" {
            mutate {
                update => { "iswithdrawn" => "1" }
            }
        }
        mutate {
            convert => {  "iswithdrawn" => "integer" }
        }
    }
    if [@metadata][TOPIC] == "openbmp.parsed.ls_link" {
        csv {
            source => ["HEADER"]
            #need to set the value of "separator" to the actual tab character and not "\t"!
            separator => "	"
            columns => ["iswithdrawn", "sequence", "hash_id", "base_attr_hash_id", "router_hash_id", "router_ip", "peer_hash_id",
                        "peer_ip", "peer_asn", "timestamp", "igp_router_id", "router_id", "routing_id", "ls_id",
                        "ospf_area_id", "isis_area_id", "protocol", "as_path", "local_pref", "med", "next_hop", "mt_id",
                        "local_link_id", "remote_link_id", "interface_ip", "neighbor_ip", "igp_metric", "admin_group",
                        "max_link_bw", "max_resv_bw", "unreserved_bw", "te_default_metric", "link_protection",
                        "mpls_proto_mask", "srlg", "link_name", "remote_node_hash_id", "local_node_hash_id",
                        "remote_igp_router_id", "remote_router_id", "local_node_asn", "remote_node_asn", "peer_node_sid",
                        "is_pre_policy", "is_adj_in", "adjacency_sids"]
            remove_field => ["HEADER", "column46", "@version", "@timestamp", "router_hash_id", "router_ip",
                             "peer_ip", "peer_asn", "routing_id", "ls_id", "ospf_area_id", "isis_area_id",
                             "as_path", "local_pref", "med", "next_hop", "is_pre_policy", "is_adj_in"]
            convert => {
                "sequence" => "integer"
                "mt_id" => "integer"
                "local_link_id" => "integer"
                "remote_link_id" => "integer"
                "admin_group" => "integer"
                "max_link_bw" => "integer"
                "max_resv_bw" => "integer"
                "te_def_metric" => "integer"
                "igp_metric" => "integer"
                "local_node_asn" => "integer"
                "remote_node_asn" => "integer"
            }
        }
        if [iswithdrawn] == "add" {
            mutate {
                update => { "iswithdrawn" => "0" }
            }
        }
        else if [iswithdrawn] == "del" {
            mutate {
                update => { "iswithdrawn" => "1" }
            }
        }
        mutate {
            convert => {  "iswithdrawn" => "integer" }
        }
    }
    if [@metadata][TOPIC] == "openbmp.parsed.ls_prefix" {
        csv {
            source => ["HEADER"]
            #need to set the value of "separator" to the actual tab character and not "\t"!
            separator => "	"
            columns => ["iswithdrawn", "sequence", "hash_id", "base_attr_hash_id", "router_hash_id", "router_ip", "peer_hash_id",
                        "peer_ip", "peer_asn", "timestamp", "igp_router_id", "router_id", "routing_id", "ls_id",
                        "ospf_area_id", "isis_area_id", "protocol", "as_path", "local_pref", "med", "next_hop",
                        "local_node_hash_id", "mt_id", "ospf_route_type", "igp_flags", "route_tag", "ext_route_tag",
                        "ospf_fwd_addr", "igp_metric", "prefix", "prefix_len", "is_pre_policy", "is_adj_in", "prefix_sids"]
            remove_field => ["HEADER", "column34", "@version", "@timestamp", "router_hash_id", "router_ip",
                             "peer_ip", "peer_asn", "igp_router_id", "router_id", "routing_id", "ls_id",
                             "ospf_area_id", "isis_area_id", "as_path", "local_pref", "med", "next_hop", "is_pre_policy",
                             "is_adj_in"]
            convert => {
                "sequence" => "integer"
                "mt_id" => "integer"
                "prefix_len" => "integer"
                "route_tag" => "integer"
                "ext_route_tag" => "integer"
                "igp_metric" => "integer"
            }
        }
        if [iswithdrawn] == "add" {
            mutate {
                update => { "iswithdrawn" => "0" }
            }
        }
        else if [iswithdrawn] == "del" {
            mutate {
                update => { "iswithdrawn" => "1" }
            }
        }
        mutate {
            convert => {  "iswithdrawn" => "integer" }
        }
    }
    if [@metadata][TOPIC] == "openbmp.parsed.l3vpn" {
        csv {
            source => ["HEADER"]
            #need to set the value of "separator" to the actual tab character and not "\t"!
            separator => "	"
            columns => ["iswithdrawn", "sequence", "hash_id", "router_hash_id", "router_ip", "base_attr_hash_id", "peer_hash_id",
                        "peer_ip", "peer_asn", "timestamp", "prefix", "prefix_len", "is_ipv4", "origin", "as_path",
                        "as_path_count", "origin_as", "next_hop", "med", "local_pref", "aggregator", "community_list",
                        "ext_community_list", "cluster_list", "is_atomic_agg", "is_next_hop_ipv4", "originator_id",
                        "path_id", "labels", "is_pre_policy", "is_adj_in", "rd", "rd_type",
                        "large_community_list"]
            remove_field => ["HEADER", "column34", "@version", "@timestamp", "sequence", "router_hash_id", "router_ip",
                                         "peer_ip", "peer_asn", "origin", "as_path", "as_path_count", "next_hop", "med",
                                         "local_pref", "aggregator", "community_list", "cluster_list", "is_atomic_agg",
                                         "is_next_hop_ipv4", "originator_id", "rd_type", "large_community_list"]
            convert => {
                "is_ipv4" => "integer"
                "origin_as" => "integer"
                "prefix_len" => "integer"
                "path_id" => "integer"
                "is_pre_policy" => "integer"
                "is_adj_in" => "integer"
            }
        }
        mutate {
            update => { "prefix" => "%{[prefix]}/%{[prefix_len]}" }
        }
        if [iswithdrawn] == "add" {
            mutate {
                update => { "iswithdrawn" => "0" }
            }
        }
        else if [iswithdrawn] == "del" {
            mutate {
                update => { "iswithdrawn" => "1" }
            }
        }
        mutate {
            convert => {  "iswithdrawn" => "integer" }
        }
        if ! [ext_community_list] {
            mutate {
                update => { "ext_community_list" => "" }
            }
        }
        mutate {
           split => [ "ext_community_list", " " ]
        }
    }
#    if [@metadata][TOPIC] == "openbmp.parsed.evpn" {
#        csv {
#            source => ["HEADER"]
#            #need to set the value of "separator" to the actual tab character and not "\t"!
#            separator => "	"
#            columns => ["action", "sequence", "hash_id", "router_hash_id", "router_ip", "base_attr_hash_id", "peer_hash_id", "peer_ip",
#                        "peer_asn", "timestamp", "origin", "as_path", "as_path_count", "origin_as", "next_hop", "MED",
#                        "local_pref", "aggregator", "community_list", "ext_community_list", "cluster_list", "is_atomic_agg",
#                        "is_next_hop_IPv4", "originator_id", "path_id", "is_pre_policy", "is_adj_in", "route_istinguisher",
#                        "type_route_istinguisher", "origin_router_ip_len", "origin_router_ip", "ether_tag_id_hex",
#                        "ether_sids", "mac_len", "mac", "ip_len", "ip", "mpls_label_1", "mpls_label_2",
#                        "large_community_list"]
#            remove_field => ["HEADER", "column40", "@version", "@timestamp"]
#        }
#    }
}

output {
    if [@metadata][TOPIC] == "openbmp.parsed.collector" {
        clickhouse {
            http_hosts =>  ["http://localhost:8123"]
            user => "<user>"
            password => "<password>"
            table => "openbmp.collector"
            automatic_retries => 3
            request_tolerance => 0
            backoff_time => 5
            flush_size => 5000
            pool_max => 5000
            save_on_failure => false
            save_dir => "/var/lib/logstash"
        }
    }
    if [@metadata][TOPIC] == "openbmp.parsed.router" {
        clickhouse {
            http_hosts =>  ["http://localhost:8123"]
            user => "<user>"
            password => "<password>"
            table => "openbmp.router"
            automatic_retries => 3
            request_tolerance => 0
            backoff_time => 5
            flush_size => 5000
            pool_max => 5000
            save_on_failure => false
            save_dir => "/var/lib/logstash"
        }
    }
    if [@metadata][TOPIC] == "openbmp.parsed.peer" {
        clickhouse {
            http_hosts =>  ["http://localhost:8123"]
            user => "<user>"
            password => "<password>"
            table => "openbmp.peer"
            automatic_retries => 3
            request_tolerance => 0
            backoff_time => 5
            flush_size => 5000
            pool_max => 5000
            save_on_failure => false
            save_dir => "/var/lib/logstash"
        }
    }
    if [@metadata][TOPIC] == "openbmp.parsed.bmp_stat" {
        clickhouse {
            http_hosts =>  ["http://localhost:8123"]
            user => "<user>"
            password => "<password>"
            table => "openbmp.bmp_stat"
            automatic_retries => 3
            request_tolerance => 0
            backoff_time => 5
            flush_size => 5000
            pool_max => 5000
            save_on_failure => false
            save_dir => "/var/lib/logstash"
        }
    }
    if [@metadata][TOPIC] == "openbmp.parsed.base_attribute" {
        clickhouse {
            http_hosts =>  ["http://localhost:8123"]
            user => "<user>"
            password => "<password>"
            table => "openbmp.base_attribute"
            automatic_retries => 3
            request_tolerance => 0
            backoff_time => 5
            flush_size => 5000
            pool_max => 5000
            save_on_failure => false
            save_dir => "/var/lib/logstash"
        }
    }
    if [@metadata][TOPIC] == "openbmp.parsed.unicast_prefix" {
        clickhouse {
            http_hosts =>  ["http://localhost:8123"]
            user => "<user>"
            password => "<password>"
            table => "openbmp.unicast_prefix"
            automatic_retries => 3
            request_tolerance => 0
            backoff_time => 5
            flush_size => 5000
            pool_max => 5000
            save_on_failure => false
            save_dir => "/var/lib/logstash"
        }
    }
    if [@metadata][TOPIC] == "openbmp.parsed.ls_node" {
        clickhouse {
            http_hosts =>  ["http://localhost:8123"]
            user => "<user>"
            password => "<password>"
            table => "openbmp.ls_node"
            automatic_retries => 3
            request_tolerance => 0
            backoff_time => 5
            flush_size => 5000
            pool_max => 5000
            save_on_failure => false
            save_dir => "/var/lib/logstash"
        }
    }
    if [@metadata][TOPIC] == "openbmp.parsed.ls_link" {
        clickhouse {
            http_hosts =>  ["http://localhost:8123"]
            user => "<user>"
            password => "<password>"
            table => "openbmp.ls_link"
            automatic_retries => 3
            request_tolerance => 0
            backoff_time => 5
            flush_size => 5000
            pool_max => 5000
            save_on_failure => false
            save_dir => "/var/lib/logstash"
        }
    }
    if [@metadata][TOPIC] == "openbmp.parsed.ls_prefix" {
        clickhouse {
            http_hosts =>  ["http://localhost:8123"]
            user => "<user>"
            password => "<password>"
            table => "openbmp.ls_prefix"
            automatic_retries => 3
            request_tolerance => 0
            backoff_time => 5
            flush_size => 5000
            pool_max => 5000
            save_on_failure => false
            save_dir => "/var/lib/logstash"
        }
    }
    if [@metadata][TOPIC] == "openbmp.parsed.l3vpn" {
        clickhouse {
            http_hosts =>  ["http://localhost:8123"]
            user => "<user>"
            password => "<password>"
            table => "openbmp.l3vpn"
            automatic_retries => 3
            request_tolerance => 0
            backoff_time => 5
            flush_size => 5000
            pool_max => 5000
            save_on_failure => false
            save_dir => "/var/lib/logstash"
        }
    }
#    if [@metadata][TOPIC] == "openbmp.parsed.evpn" {
#        clickhouse {
#            http_hosts =>  ["http://localhost:8123"]
#            user => "<user>"
#            password => "<password>"
#            table => "openbmp.evpn"
#            automatic_retries => 3
#            request_tolerance => 0
#            backoff_time => 5
#            flush_size => 5000
#            pool_max => 5000
#            save_on_failure => false
#            save_dir => "/var/lib/logstash"
#        }
#    }
}
```
