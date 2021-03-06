..
 This work is licensed under a Creative Commons Attribution 3.0 Unported
 License.

 http://creativecommons.org/licenses/by/3.0/legalcode

=================================
Stable Keystone Driver Interfaces
=================================

`bp stable-driver-interfaces
<https://blueprints.launchpad.net/keystone/+spec/stable-driver-interfaces>`_


Keystone has a number of backend drivers that are purportedly able to be
replaced by a developer or deployer with their own implementation (e.g.
utilizing mongodb as a store for Identity information). Currently these
drivers have had significant interface changes each cycle making it difficult
for developers to maintain custom (or subclassed) drivers as each release
has caused a significant delta in all of the Keystone Driver Interface
definitions.

Problem Description
===================

To properly support developers who are implementing drivers for Keystone out
of tree, the Keystone Driver Interface need to be stable like the
REST API is. This specification is to commit to the interface for each driver
and ensure that drivers that are written against Liberty will work with
the M-Release of Keystone as well (a minimum of 2-cycle Interface commitment).

Changes to a given driver interface will require compatibility code (to be
provided by the developer that is proposing the change) to ensure that the
supported window of stability is maintained. This means that when a driver
interface change is proposed (via a new version for the specific subsystem),
Keystone will need appropriate logic to work with both the new version and
any currently supported version.

Proposed Change
===============

Each subsystem will have it's driver ABC Base class looked at for a redesign.
The keystone stable driver interface definitions will be versioned and
Keystone will ensure that it can load any version of the driver interface.

Alternatives
------------

Alternatives include "trying" to ensure we don't break the driver interface
[best effort] or continuing with the current way of allowing interfaces to
change between releases. This however, is a sub-optimal experience for
deployers and developers.

Security Impact
---------------

Changes to the driver interfaces to address Security concerns could become more
difficult. There should be no direct security impact. Each driver interface
definition will need to be reviewed, but this is the same as any change
impacting a given driver interface.

Notifications Impact
--------------------

No notification changes should be needed.

Other End User Impact
---------------------

No changes to end users.

Performance Impact
------------------

No expected performance changes.

Other Deployer Impact
---------------------

Deployers will be able to utilize drivers for more versions of Keystone than
before. However, there should be minimal deployer impact.

Developer Impact
----------------

Developers will need to be aware of how to change the driver interface
definitions. This will include needing to develop the compatibility layer if
a driver interface needs to be changed so previous versions of the driver can
be loaded.


Implementation
==============

Assignee(s)
-----------

Primary assignee:

  * gyee (Guang Yee)
  * ajayaa (Ajaya Agrawal)
  * rushiagr (Rushi Agrawal)

Work Items
----------

  * Evaluate and develop the stable interfaces for the following subsystems:

  * Catalog

  * Resource

  * Identity

  * Assignment

  * Assignment.Roles

  * Credential

  * Token Persistence

  * Token Provider

  * Policy

  * Federation

  * OAuth

  * Endpoint Policy

* Convert current drivers to the new driver interface definitions

* Create a separate repo or suite of tests that implements a base (just simple)
  version of the drivers that can be used for validation / loading to ensure
  compatibility / loading works as expected when/if the interface changes.

Dependencies
============

None


Documentation Impact
====================

Documentation on how to update the driver interfaces and what is expected in
compatibility will be needed. Clear indication of the driver interface
definitions will need to be clearly indicated in our documents.


References
==========


