========
Examples
========


Establishing a connection:

.. code-block :: python

    >>> from pystassh import Session
    >>> # With default private key
    >>> session = Session('remote_host.org')
    >>> # With username and password
    >>> session = Session('remote_host.org', username='foo', password='bar')
    >>> # With specific private key and a passphrase
    >>> session = Session('remote_host.org', privkey_file='/home/user/.ssh/my_key', passphrase='baz')


Running simple commands:

.. code-block :: python

    >>> from pystassh import Session
    >>> with Session('remote_host.org') as ssh_session:
    ...     res = ssh_session.execute('whoami')
    >>> res.stdout
    'foo'

Handling errors:

.. code-block :: python

    >>> from pystassh import Session
    >>> with Session('remote_host.org') as ssh_session:
    ...     res = ssh_session.execute('whoam')
    >>> res.stderr
    'bash: whoam : command not found'

Running multiple commands:

.. code-block :: python

    >>> from pystassh import Session
    >>> with Session('remote_host.org') as ssh_session:
    ...     ssh_session.execute('echo "bar" > /tmp/foo')
    ...     res = ssh_session.execute('cat /tmp/foo')
    >>> res.stdout
    'bar'

Use a session without a ``with`` block:

.. code-block :: python

    >>> from pystassh import Session
    >>> ssh_session = Session('remote_host.org')
    >>> ssh_session.connect()
    >>> res = ssh_session.execute('whoami')
    >>> res.stdout
    'foo'
    >>> ssh_session.disconnect()
