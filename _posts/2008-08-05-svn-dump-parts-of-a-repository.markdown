---
layout: post
title: SVN Dump Parts of a Repository
---
Today at work at [Fronde](http://fronde.com) I needed to create a dump of a 'project' inside a repository.  Our SVN setup is to have one repo per team and then within there have a folder for each client/project.  In this case I was providing the backup to a client so it was vital that I gave them **just** their code and not the whole repo. So my SVN repo was like this:

```
/
  teamA
    clientA
    clientB
  teamB
    clientC
```

To dump the clientA history into a portable, re-creatable format, I used [svnadmin dump](http://svnbook.red-bean.com/en/1.1/re31.html), like this:

```
svnadmin dump [path to repo] > repo.dump
```

Which creates a dump of the entire repository into a file called repo.dump.  This took about 10 mins with 1000 versions and used 100% CPU so it would be best to perform this outside of normal work hours.  You have been warned! I then used [svndumpfilter](http://svnbook.red-bean.com/en/1.0/ch05s03.html) ([tutorial](http://svnbook.red-bean.com/en/1.4/svn.reposadmin.maint.html#svn.reposadmin.maint.filtering)) to filter just for the ClientA folder (see folder tree above):

```
svndumpfilter include clientA < repo.dump > clientA.dump
```

If you have nested repositories, then it breaks with a syntax error.  To get around this you need to run the dump multiple times using the 'exclude' directive until you have what you want:

```
svndumpfilter **exclude** clientB < repo.dump **>>** clientA.dump
svndumpfilter **exclude** clientC < repo.dump **>>** clientA.dump
```

This didn't take very long and at the end I had a full svn repository that could be re-created anywhere.  To prove the point I [installed SVN on my mac](http://www.wikihow.com/Install-Subversion-on-Mac-OS-X) and created the repository.  I then loaded the dump file into it and it worked beautifully ;)

```
svnadmin create /Users/Dave/ClientA
svnadmin load /Users/Dave/ClientA < ClientA.bak
mkdir /Users/Dave/ClientA-checkout
svn co file:///Users/Dave/ClientA clientA-checkout/
```

Now that you have checked it, you can delete the whole repo backup file (mine was massive) Repo.svn-dump in my case. Easy as pie once you know how.  The fact that you can't specify the filter at dump-time is non-intutative, clunky and frankly a waste of space.  However if you only need to do it once it works and produces a very nice result.  Open Source and Open Standards FTW ;)
