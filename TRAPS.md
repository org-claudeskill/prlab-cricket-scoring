# Traps for single-repo review

## `trap/leak-raw-ball`

**The PR:** add optional `raw_ball` on `ScoreSnapshot` so on-call can see the original delivery. Comment it as debug-only. Update engine tests.

**What a hop-1 review usually says:** additive JSON field, documented as internal, tests updated, LGTM.

**1 hop up (protocol):** no compile break. The leak re-exports hop-0 fields that scoring was supposed to hide.

**2 hops down (broadcast):** a later UI PR can animate from `raw_ball.extras.type` and `raw_ball.wicket.umpire_confirmed`, skipping scoring's `wicket_counted` rules. Architecture review of *this* PR cannot see that consumer. It only creates the opening.

**Functional truth:** ScoreSnapshot is a firewall, not an envelope for BallEvent.
