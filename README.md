Notes on Python Memory Leaks
=======

Tools
-----------

**pdb** [Link] (https://docs.python.org/2/library/pdb.html)

**Heapy** [Link] (http://guppy-pe.sourceforge.net/#Heapy)

**ObjGraph** [Link] (http://mg.pov.lt/objgraph/)

**Memtop** [Link] (https://pypi.python.org/pypi/mem_top)

**Muppy** [Link] (https://pythonhosted.org/Pympler/muppy.html)

Heroku
-----------
 
Memory Interpretation:

* **Resident Memory** (memory_rss): The portion of the dyno’s memory (megabytes) held in RAM.
* **Disk Cache Memory** (memory_cache): The portion of the dyno’s memory (megabytes) used as disk cache.
* **Swap Memory** (memory_swap): The portion of the dyno’s memory (megabytes) stored on disk. Swapping is extremely slow and should be avoided.
* **Total Memory** (memory_total): The total memory (megabytes) being used by the dyno, equal to the sum of resident, cache, and swap memory.

Articles
-----------
http://chase-seibert.github.io/blog/2013/08/03/diagnosing-memory-leaks-python.html

http://www.lshift.net/blog/2008/11/14/tracing-python-memory-leaks/

http://mflerackers.wordpress.com/2012/04/12/fixing-and-avoiding-memory-leaks-in-python/

http://www.huyng.com/posts/python-performance-analysis/

Notes for myself
-----------

* Look at a possible C module integrated into Python leaking memory;
* Messing up with big files on Heroku will trigger R14 Alerts because of the memory_cache usage;
* Look for circular references;
* Look for enabled logs in production;
* Look for modules overwriting the __del__ destructor;
* Silly script do debug memory problems
```
while true
do
echo "---------------------------------" >> ~/mem_usage.txt
date >> ~/mem_usage.txt
ps aux >> ~/mem_usage.txt
sleep 60
done
```
