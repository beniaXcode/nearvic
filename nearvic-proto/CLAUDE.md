# nearvic-proto — Context

## What this crate is
Shared library with all protocol types, frame definitions, serialization,
and constants used by BOTH nearvic-client and nearvic-agent.

## Rules — strictly enforced
- Zero hardware dependencies — this must compile on any target
- No tokio, no async — pure data types and serialization only
- All types must implement Serialize + Deserialize (serde)
- All changes here affect BOTH client and agent — think twice
- Backward compatibility matters — never remove fields, only add

## What lives here
- FrameHeader struct (stream_type, flags, seq, timestamp_ms, payload_len)
- InputPacket struct (device, seq, timestamp + payload)
- Stream type constants (video=0, audio=1, input=2, file=3, usb=4)
- Error types shared across both binaries
- Connection handshake types

## Gotchas
- Keep types #[repr(C)] where they are sent over the wire
- Document every field — these types are the contract between client and agent