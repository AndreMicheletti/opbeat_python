Configuring ZeroRPC
===================

.. csv-table::
  :class: page-info

  "Page updated: 23rd July 2013", ""

Setup
-----

The ZeroRPC integration comes as middleware for ZeroRPC. The middleware can be
configured like the original opbeat client (using keyword arguments) and
registered into ZeroRPC's context manager

.. code::
    :class: language-python

    import zerorpc

    from opbeat.contrib.zerorpc import OpbeatMiddleware

    opbeat = OpbeatMiddleware(organization_id='<org-id>', ...)
    zerorpc.Context.get_instance().register_middleware(opbeat)

By default, the middleware will hide internal frames from ZeroRPC when it
submits exceptions to Opbeat. This behavior can be disabled by passing the
``hide_zerorpc_frames`` parameter to the middleware

.. code::
    :class: language-python

    opbeat = OpbeatMiddleware(hide_zerorpc_frames=False, organization_id='<org-id>', ...)

Caveats
-------

Sending an exception to Opbeat will basically block your RPC call.
In any cases, a clean and long term solution would be to make opbeat requests
to the Opbeat server asynchronous.
