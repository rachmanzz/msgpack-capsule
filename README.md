# msgpack-capsule

`msgpack-capsule` is a lightweight library designed for use with **HonoWS**, a WebSocket library for **Hono**. It provides efficient message serialization and deserialization using `msgpack-lite`, ensuring smooth communication between backend and frontend applications.

The library focuses on encapsulating messages in standard formats, which can be transmitted via WebSockets, while leveraging the benefits of `msgpack-lite` for compact binary data serialization.

---

## Features
- **Efficient message serialization and deserialization** using `msgpack-lite`.
- Designed for use with **HonoWS**, a WebSocket library for **Hono**.
- Provides **standard message formats** for different data types: `Text`, `Object`, `Audio`, and `Video`.

---

## Installation

To install `msgpack-capsule`, run:

```bash
npm install msgpack-capsule
```

---

## API Documentation

### `serialCapsule(data: TypeSerialCapsule): Buffer | null`
Encapsulates structured data into an optimized binary format.

#### Arguments:
- `data`: The data to be serialized, which should be one of the following types:
  - `TextSerial`
  - `ObjectSerial`
  - `VideoSerial`
  - `AudioSerial`

#### Returns:
- A `Buffer` representing the serialized data in `msgpack` format.
- `null` if the content does not match the specified MIME type or is invalid.

### `deserialCapsule(data: Buffer | Uint8Array | number[]): TypeSerialCapsule | null`
Reconstructs messages from binary format using `msgpack-lite`.

#### Arguments:
- `data`: The data to be deserialized (can be a `Buffer`, `Uint8Array`, or `number[]`).

#### Returns:
- A reconstructed object of type `TypeSerialCapsule`.
- `null` if deserialization fails.

### Supported Message Types

`msgpack-capsule` supports several structured message types. Below are the available types:

#### `TextSerial`
```ts
export type TextSerial = {
  mime: "text/plain",
  content: string,
  verifier?: string
};
```

#### `ObjectSerial`
```ts
export type ObjectSerial = {
  mime: "application/json",
  content: object,
  verifier?: string
};
```

#### `AudioSerial`
```ts
export type AudioSerial = {
  mime: "audio/wav" | "audio/mpeg" | "audio/ogg" | "audio/mp4",
  content: ArrayBuffer | Uint8Array,
  verifier?: string
};
```

#### `VideoSerial`
```ts
export type VideoSerial = {
  mime: "video/mp4" | "video/webm" | "video/ogg" | "video/mpeg",
  content: ArrayBuffer | Uint8Array,
  verifier?: string
};
```

### `TypeSerialCapsule`
```ts
export type TypeSerialCapsule = TextSerial | ObjectSerial | VideoSerial | AudioSerial;
```

---

## Usage Example

```ts
import { serialCapsule, deserialCapsule } from "msgpack-capsule";

// Example data to be serialized
const textData = {
  mime: "text/plain",
  content: "Hello, World!"
};

// Serialize the message
const serializedMessage = serialCapsule(textData);

// Deserialize the message
if (serializedMessage) {
  const deserializedMessage = deserialCapsule(serializedMessage);
  console.log(deserializedMessage);  // { mime: "text/plain", content: "Hello, World!" }
}
```

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

### Notes:
- This library is intended for use with **HonoWS** (WebSocket library for Hono) for backend communication.
- The API follows a structure similar to how HonoWS serializes messages, providing compatibility for efficient serialization and deserialization in backend and frontend applications.

---
