.. |labmodule| replace:: 4
.. |labnum| replace:: 3
.. |labdot| replace:: |labmodule|\ .\ |labnum|
.. |labund| replace:: |labmodule|\ _\ |labnum|
.. |labname| replace:: Lab\ |labdot|
.. |labnameund| replace:: Lab\ |labund|

Test Cases
----------

The |appsvcs| package includes a comprehensive test framework that uses the 
:ref:`helper_deploy_iapp` helper script to test the functionality of the
template. 

The use cases are contained within the :github_file:`test <test>` directory of
the source tree.  The ``.json`` files within this directory represent the input
variables used to test the specific use case.

Users of the |appsvcs| template can refer to the test case JSON files as the 
authoritative source for implemented functionality.  The :doc:`/presoref` also
includes links to each test case that references a particular input variable.  
By examining the test case templates a user can determine additional 
functionality that is available but has not been covered in a specific lab.

Developers interested in running the test framework would use the 
:github_file:`run_tests.py <test/run_tests.py>` script.  The script can 
be run with the ``--help`` option to obtain more information.

To run the complete test framework the following prerequisite steps are 
required:

.. NOTE::
   The test script currently requires unix-style utilities (scp/ssh).  Linux
   and Mac OS have these utilities installed or available.  To run the test
   framework on a Windows system please install 
   `Cygwin <https://www.cygwin.com/>`__.

#. Provision your BIG-IP device with the following modules in at a 'nominal' 
   level:

    - LTM
    - APM
    - ASM
    - AFM

#. Configure NTP and DNS servers on the BIG-IP system.  DNS servers should be
   able to resolve internet host names.

#. Untar :github_file:`remote_url_files.tar.gz <test/remote_url_files.tar.gz>` 
   to the root of a webserver.  

#. Provide the IP address of the server to 
   :github_file:`run_tests.py <test/run_tests.py>` with the ``-b <IP Address>`` 
   option.

#. Build the template using the command ``python build.py -nd -b test/bundled.test``

#. Upload the template to the BIG-IP (:ref:`helper_deploy_iapp` can be used)

#. Monitor the deployment log on BIG-IP using ``tail –f /var/tmp/scriptd.out``
 
If you are running our functional tests you will need a real BIG-IP® to run
them against, but you can get one of those pretty easily in [Amazon EC2](https://aws.amazon.com/marketplace/pp/B00JL3UASY/ref=srh_res_product_title?ie=UTF8&sr=0-10&qid=1449332167461).
