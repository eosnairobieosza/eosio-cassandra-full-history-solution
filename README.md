# EOSIO CASSANDRA FULL HISTORY SOLUTION

EOSIO full history services are not critical for the functioning of the EOS blockchain. They are, however, critical for dApps such as block explorers and wallet applications that are essential for mass adoption. The original EOSIO shipped with a proprietary history API served by a nodeos plugin. Although this served its purpose at network launch it has become increasingly difficult to maintain. The original history plugin has now been deprecated. The functions performed by this plugin are now performed by the state history plugin and the MongoDB plugin. Both of these solutions serve the current needs of the EOS ecosystem but suffer from performance and reliability problems. System failures can be recovered by doing a blockchain replay but this is becoming increasingly difficult and time consuming as the blockchain grows.
We therefore propose a more scalable and reliable open source solution for the general health of the blockchain. 

## Why Cassandra 

We seek to accomplish the task of providing the community with a scalable full history solution using Cassandra for the following reasons:
*Cassandra offers true horizontal scaling. As the cluster grows performance improves.
*Cassandra query performance is consistent and predictable (i.e. the same query will return repeatedly within approximately the same time). This results in a consistent user experience.
*All Cassandra nodes are the same. All that is needed to expand the system is to add new nodes to the cluster. Similarly nodes can be removed by retiring them from the cluster. Data is rebalanced within the cluster as nodes are added and removed.
*The Cassandra architecture includes redundancy by design. The cluster is initialized with a desired redundancy factor. The system itself manages data replication to achieve the desired redundancy levels. If a node failure is experienced the cluster will rebalance to maintain the desired redundancy level.
Because Cassandra handles redundancy at a system level nodes can be built with commodity hardware which need not include node level redundancy (use RAID, dual power supplies, etc). The financial savings achieved by utilizing commodity hardware and not needing node level redundancy mitigate the cost of storing multiple copies of data in the system.
*Cassandra nodes employ data compression when storing data. This compression results in raw storage requirements being roughly the same as would be required to store uncompressed data without compression for sensible redundancy factors. (i.e. nett result of compression plus redundancy is approximately nill) This is a general statement and is obviously dependent on redundancy factor used and compressibility of raw data.
*Cassandra is rack and data center aware. Nodes can be distributed in multiple racks and in multiple data centers. Data will automatically be distributed efficiently between remote nodes.


## Technical references

A considerable amount of work has been done by the EOS community on solutions to the full history. This project will draw on the work done by other teams in order to mitigate project risks. Notable references are;
* [EOSIO RPC API developers reference](https://developers.eos.io/eosio-nodeos/reference) - This reference defines the history API endpoints.
* [EOSIO history plugin] (https://github.com/EOSIO/eos/tree/master/plugins/history_plugin)- Original EOS history plugin.
* [EOSIO history API plugin, https://github.com/EOSIO/eos/tree/master/plugins/history_api_plugin
Original EOSIO history API plugin.
* [EOSIO MongoDB plugin, https://github.com/EOSIO/eos/tree/master/plugins/mongo_db_plugin
The EOSIO MongoDB plugin which was created to replace the (deprecated) history and history API plugins.
* [Greymass hapi branch of history plugin, https://github.com/greymass/eos/tree/hapi-production/plugins/history_plugin
Modifications to the EOSIO history plugin which resolve shortcomings in the original EOSIO history plugin by splitting the history file into multiple smaller files. This allows the history plugin to continue working on the EOS mainnet.
* [EOS Lao Mao Elasticsearch plugin, https://github.com/EOSLaoMao/elasticsearch_plugin
An alternative “DB” plugin by EOS Lao Mao which allows history records to be stored in Elasticsearch instead of MongoDB. Benchmarks show approximately 250% performance improvements over MongoDB.
* [Atticlab Elasticsearch history API, https://github.com/atticlab/eos-es-historyapi
An EOS history API by Atticlab based on Elasticsearch and built using GO. Something similar will be required to deliver history API services on Cassandra.
* [Public work proposals for EOS infrastructure, EOS Chronicle Project], (https://github.com/EOSChronicleProject/eos-chronicle)
* [EOS zmq Plugin Receiver](https://github.com/cc32d9/eos_zmq_plugin_receiver)
* [EOS zmq Plugin](https://github.com/cc32d9/eos_zmq_plugin)


## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/dkimotho/2b955a274fbc483e71dcea6b39996ad8) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/your/project/tags). 

## Authors

* **Rory Mapstone** - *EOS ZA* - [EOS ZA](https://eosza.io/)
* **Daniel Kimotho** - *EOS Nairobi* - [EOS Nairobi](http://eosnairobi.io)



## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* EOS CVIB - started with the vision for proxies to explicitly signal intent to vote for BPs, for a given time frame, on the basis of specific projects being built.
* EOS Proxy Voter Community
