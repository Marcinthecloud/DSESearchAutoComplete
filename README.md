# DSE Search Simple Autocomplete
![Alt text](http://i.imgur.com/ATeiogp.png)

This is an extension of the Amazon Book Solr Demo to show how to do simple Autocomplete. I am by no means an HTML expert, in fact I've never really used it before this demo so there's going to be lots of changes/improvements coming in the future.

#####Prerequisites
* Python 2.7+
* [DataStax Python Driver](https://github.com/datastax/python-driver)
* >Note you may have to sudo apt-get install gcc
* [DataStax Enterprise 4.7.3 or greater](https://www.datastax.com/downloads)

#####How-to:
1. Start DataStax Enterprise in search mode
  * ```for tarball installs: bin/dse cassandra -s```
  * ```for package installs: set SOLR=1 in the dse.default file and run: service dse start```
2. Run ```SearchData/solr_dataloader.py```
  * This will create the CQL schemas and load the data
3. Run ```SearchData/create_core.sh```
  * This will generate Solr cores and index the data
4. Drag and drop or mv the entire 'autocomplete' folder to ```resources/solr/web/demos/```
5. Access the autocomplete demo from: http://localhost:8983/demos/autocomplete/dsesearch.html

#####Under the Hood

This demo uses a combination of jquery, ajax, and the DSE Search REST API. jquery and ajax are used as place holders as I'll eventually be moving to some more custom code.

The demo uses this REST command: ```http://localhost:8983/solr/amazon.metadata/select?q=title:*&fl=title&wt=json```
Which returns:

```javascript
{"responseHeader":{"status":0,"QTime":8},"response":{"numFound":10582,"start":0,"docs":[{"title":"Oils (Collins 30-Minute Painting) (30 Minute Art (Collins))"},{"title":"Propellerhead"},{"title":"Enhancing Teaching"},{"title":"It s Just a Date: A Guide to a Sane Dating Life"},{"title":"Advanced Tactical Fighters (Jane's Pocket Guide)"},{"title":"More Than A Game: The Story of Cricket's Early Years"},{"title":"Hortus Third: A Concise Dictionary of Plants Cultivated in the United States and Canada"},{"title":"The Arab Boycott of Israel: Economic Aggression and World Reaction"},{"title":"The deadly stroke"},{"title":"Zigby Dives In"}]}}
```
