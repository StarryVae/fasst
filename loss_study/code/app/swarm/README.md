## Postlist and slack
We can get up to `O(WINDOW_SIZE + (NUM_SERVERS * PER_SERVER_CREDITS)`
completions in every `poll_cq()`, consisting of both new requests and responses.
We break down the response send()s into postlists of size `@postlist`. New
requests are sent out in non-postlist send()s if `USE_REQ_POSTLIST == 0`.

## Port mapping
 * A worker receives new requests on its primary port `wrkr_gid % num_ports`
only; responses are also sent out only on this port.
 * Responses are received on both ports.
 * All RECVs are posted on 0th QP on each port.


