=======================================
NDN Project Code Review System Document
=======================================

Initialization
==============

1. Create account on `gerrit.named-data.net`_.

.. _gerrit.named-data.net: http://gerrit.named-data.net/

2. Add the project you want to watch. Click your ID in the upper right corner -> *Settings* -> *Watched Projects*.


Setup Project For Code Review on Gerrit
=======================================

Create a brand new project
--------------------------

Click *Projects* -> *Create New Project*. 
You can create a remote repo on Gerrit with an initial commit.
You can clone the repo using the URL listed on the *General* page of the project.
For example, 

::

  git clone ssh://<username>@gerrit.named-data.net:29418/ndnx

You cannot create a project without corresponding access privilege.

Import an existing repo a new project
-------------------------------------

Create a new project in the same way above (without an initial commit). 
Add the Gerrit repo as a remote repo.
For example,

::

  git remote add gerrit ssh://<username>@gerrit.named-data.net:29418/ndnx

Push existing repo directly to Gerrit repo.

::

  git push gerrit <branch_name>:refs/heads/<branch_name>

This can help you to bypass the code view for all the previous commits.

  
Set project ACL
---------------

For each project, there are two user groups: project owner and contributor.

Project owner has full access to the project including submitting the final changes.
Contributor can upload changes and make reviews.

System administrator can assign users into appropriate groups.


To Upload Changes
=================

1. Add the corresponding Gerrit repo as one of your remote repo, e.g.,

::
  
  git remote add gerrit ssh://<username>@gerrit.named-data.net:29418/ndnx

You can find the URL of the Gerrit repo from `gerrit.named-data.net`_.
Click *Projects* -> *List* -> *<project_name>*.

2. Install *commit-msg* hook in your local Git repo.

::

  scp -p -P 29418 <username>@gerrit.named-data.net:hooks/commit-msg .git/hooks/

ensure that the execute bit is set on the hook script:

::

  chmod u+x .git/hooks/commit-msg

3. Make your changes and commit to your local Git repo.

4. Submit your change to Gerrit repo.

::

  git push gerrit HEAD:refs/for/<branch_name>


To Review Changes
=================

1. Once a change has been uploaded, reviewers who are watching the project will be notified. 
Reviewers can find changes at *My* -> *Changes* on `gerrit.named-data.net`_.

2. Reviewer can make comments about changes and rate changes from -2 to +2. 
-1 and +1 reflect opinion only, and do not count as rejection or approval.
In order for a change to be accepted, it must have at least one +2 and no -2 votes.
Although these are numeric values, they in no way accumulate; two +1s do not equate to a +2.

To Re-work On Changes
=====================

1. Developer can checkout the original changes and re-work on it.

2. After that, developer can revise the original changes

::

  git commit --amend

3. Then developer can upload the revised changes to gerrit again.

::

  git push gerrit HEAD:refs/for/<branch_name>

To Submit Changes
=================

1. Once all the contributors and project owners have reviewed the change, and the review result is good enough (i.e., at least one +2 and no -2), 
project owner can finalize the change by submit it through `gerrit.named-data.net`_.

2. Project owner should also be responsible to synchronize the Gerrit repo with a public repo (e.g., Github repo).
