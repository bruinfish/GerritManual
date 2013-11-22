=======================================
NDN Project Code Review System Document
=======================================

Initialization
==============

1. Create account on `gerrit.named-data.net`_.

.. _gerrit.named-data.net: http://gerrit.named-data.net/

2. Add the project you want to watch. Click your ID in the upper right corner -> Settings -> Watched Projects.

To Be A Committer
=================

1. Add the corresponding Gerrit repo as one of your remote repo, e.g.,

::
  
  git remote add gerrit ssh://yingdi@gerrit.named-data.net:29418/ndnx

You can find the URI of the Gerrit repo from `gerrit.named-data.net`_.

2. Install *commit-msg* hook in your local Git repo.

::

  scp -p -P 29418 yingdi@gerrit.named-data.net:hooks/commit-msg .git/hooks/

3. Make your changes and commit to your local Git repo.

4. Submit your change to Gerrit repo.

::

  git push gerrit HEAD:refs/for/<branch_name>

