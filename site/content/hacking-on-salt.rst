Hacking on Salt (My PyCon Day 1 Sprint Experience)
##################################################

:date: 2014-04-14
:author: Sean Zicari
:summary: My efficient setup for hacking on salt
:category: sysadmin
:slug: hacking-on-salt

Overview
========

PyCon ended yesterday, sprints began today. I was very excited to hack on salt,
because it's a tool I really like to use. My initial setup involved checking out
the code on my laptop and setting it up to run "locally" (meaning it runs as my
user and uses config files in non-standard places). I really didn't like this
approach though, because even though salt wasn't running as root, I still felt
like I could accidentally do some damage or pollute my laptop during
development. So, I decided to set up my dev environment in a virtual machine.

The Setup
=========

I used vagrant with a `precise64` box, using VirtualBox as the hypervisor. This
is not an uncommon setup for me, as I use a similar setup for my side work.
These are the steps I took:

#. Install `vagrant`_, `VirtualBox`_ and `virtualenv-burrito`_
#. Download the `precise64` box
#. Spin up a new VM
#. SSH into the new VM
#. Generate a new SSH keypair for the `vagrant` user
#. Associate the public key with my GitHub user account
#. Check out the code on the VM
#. Create a new virtualenv (I called it `salt`)
#. Run through the salt setup steps outlined in the `salt setup doc`_.
#. Exit the virtual machine
#. Create an SSHFS mount of the VM's code checkout on the host machine
#. Create a virtualenv on the host machine
#. Follow the same setup steps above, using the SSHFS-mounted code
#. Set up a new project in PyCharm and point it to the host machine's virtualenv

.. _vagrant: http://www.vagrantup.com/
.. _VirtualBox: https://www.virtualbox.org/
.. _virtualenv-burrito: https://github.com/brainsik/virtualenv-burrito
.. _salt setup doc: https://github.com/saltstack/salt/blob/develop/HACKING.rst

I found this setup to be very useful, because I could do whatever I want to in
the virtual machine without harming the host, but I also don't have to pay for
the full version of PyCharm to take advantage of its excellent introspection
capabilities. PyCharm Professional comes with the capability to interface with a
remote python interpreter, so with that I would not have had to SSHFS mount the
code to the host and run through the salt setup steps twice, but I'm more
excited about the learned abilities more than the minor time savings.

I hope this helps someone.

