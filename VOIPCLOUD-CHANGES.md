# VoipCloud modifications to linphone-sdk 5.5.19

This is a modified version of **linphone-sdk 5.5.19** (upstream: https://gitlab.linphone.org/BC/public/linphone-sdk, commit `8e1ec723a2091854e3f6c19790fd64cbb7667539`). It is published to provide the corresponding source of the VoipCloud iPhone app, and it is licensed under the same terms as upstream (GNU Affero General Public License v3; see the license files in this tree, which are unchanged).

**Modified by:** ThinkSwift (VoipCloud softphone), on 19 November 2026.

## What was changed
A "bound interface" setting lets an application choose the network interface the SDK's sockets use (`IP_BOUND_IF` / `IPV6_BOUND_IF`). 0 (the default) means no pinning and the stock behaviour.

| File | Change |
|---|---|
| `bctoolbox/include/bctoolbox/vconnect.h` | New API: `bctbx_set_bound_interface`, `bctbx_get_bound_interface`, `bctbx_socket_apply_bound_interface` |
| `bctoolbox/src/vconnect.c` | Implementation; `bctbx_socket()` applies the setting and fails closed |
| `bctoolbox/src/utils/port.c` | Local-address probe uses `bctbx_socket()` |
| `bctoolbox/tester/port.c` | "Bound interface" test |
| `ortp/src/rtpsession_inet.c` | RTP/RTCP sockets use `bctbx_socket()` |
| `belle-sip/src/dns/dns.c` | Embedded DNS resolver uses `bctbx_socket()` |
| `mediastreamer2/src/base/mtu.c`, `mediastreamer2/src/voip/turn_tcp.cpp` | MTU probe and the outgoing TURN-over-TCP socket |
| `liblinphone/src/nat/stun-client.cpp` | STUN client socket |

The same changes are available as patch files (one per module) with the build script in the VoipCloud app repository, folder `ios/sdk_patch`. To build: use that folder's `build_patched_sdk.sh`, or build this tree with the upstream instructions.
