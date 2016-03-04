# Groupcash: A Commodity-Backed Cryptographic Complementary Currencies System

The goal of *groupcash* is to make it easier, cheaper and safer for anybody to run their own complementary currency.

For that it defines a set of **specifications** on which compatible **software systems** can be built which can be used for managing and trading in different kinds of independently run **currencies**.

The following figure illustrates this structure which is also the structure of this document.

![structure](http://cdn.rawgit.com/groupcash/core/94fd4e2b/figures/structure.svg)


## Currencies

Complementary currencies are a great **tool to solve** many different kind of **problems**, so they come in different forms and shapes. Which problems there are and how they are solved with *groupcash*, you can read in the [manifesto](manifesto.md).

How different **kind of currencies** solving different problems can be run with *groupcash* is described in the [use-cases](usecases.md) document.

If a complementary currency can be successfully implemented and run in depends on the community but also on the software systems and specifications. An attempt to list the underlying assumptions with the goal of collecting knowledge about pitfalls and **challenges** can be found [here](challenges.md).

The commonality of all *groupcash* currencies is that they're **commodity-backed**, meaning that they are based on delivery promises of goods or services. Forgery and fraud is prevented by [**cryptographic**][cryptography] algorithms (i.e. **math + computers**) instead of coins, bills and banks - decreasing the cost of starting and running a secure currency.

![pillars](http://cdn.rawgit.com/groupcash/core/94fd4e2b/figures/pillars.svg)

[cryptography]: https://blog.vrypan.net/2013/08/28/public-key-cryptography-for-non-geeks/


## Software Systems

While complementary could be and were run manually for many thousand years, software can make the task a lot easier and cheaper. And because of its cryptographic property, *groupcash* currencies require computers and software.

The same property allows for a wide range of different architectures. Because no central database is needed, currencies can be run in a [peer-to-peer][p2p] network or in a [server/client] architecture, with either native clients or as a web application.

Software systems implementing the *groupcash* specification can be found on the web (as soon as they exist) and are also collected in the [*groupcash* organization on github][github]

[p2p]: https://en.wikipedia.org/wiki/Peer-to-peer
[server/client]: https://en.wikipedia.org/wiki/Client%E2%80%93server_model
[github]: https://github.com/groupcash


## Specifications

The core of *groupcash* is a set of specifications that facilitate interoperability between software systems with which currencies can be run. These specify a [**design**](specifications/design.md), based on digital signatures, the [**algorithms**](specifications/algorithms.md) to create and verify these signatures, [**protocols**](specifications/protocols.md) for trading between systems and [**formats**](specifications/formats.md) how currency units and other objects can be represented virtually and physically.


## Related projects

While its approach and implementations are (hopefully) unique, *groupcash* is not the only project trying to make complementary currencies more approachable. If you know would like to add to this list or are interested in collaborating, please [contact us](http://groupcash.org/#contact).

- [MetaCurrency Project](http://metacurrency.org/) - "The MetaCurrency Project is building the tools and technology platforms to open source the next economy."
- [OpenMoney](http://openmoney.org/) - "Open money is a means of exchange freely available to all. Any community, any association - indeed, any body - can have their own money."
- [CommunityForge](http://communityforge.net/en) - "Community Forge is a non-profit organization that designs, develops and distributes tools around complementary currencies."

## Resources

- [Complementary Currency Resource Center](http://complementarycurrency.org/) - "We collaborate on the design, implementation, research and best practices in complementary currency systems."
- [Complementary Currency Literature](http://cc-literature.de/)  - "This bibliography strives to reflect the variety of research about community currencies."
- [RegioGeld](http://regionetzwerk.blogspot.de/) - Supporting local currencies in Germany
- [The Social Trade Organisation](http://www.socialtrade.nl/) - "[STRO] is one of the few organisations in the world that developes alternatives for the monetary system."
- [IRTA](http://www.irta.com/) - "IRTA is committed to promoting just and equitable standards of practice and operation within the Modern Trade and Barter and other Alternative Capital Systems Industry"
- [Qoin](http://www.qoin.org/) - "Qoin implements, manages and supports community currencies around the world."
- [The Ecology of Money](http://www.feasta.org/documents/moneyecology/contents.htm) - by Richard Douthwaite
- [People Money](http://www.lietaer.com/writings/books/people-money/) - by Margrit Kennedy, Bernard Lietaer, John Rogers
- [List of Local Currencies](https://en.wikipedia.org/wiki/Local_currency#List_of_local_currencies) - Wikipedia
- [Complementary Currency](https://en.wikipedia.org/wiki/Complementary_currency) - Wikipedia
