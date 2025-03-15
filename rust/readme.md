## Explanation of the Code

**Key Features**
- Structs for Classes: 
  - `Entity`, `Activity`, and `Agent` are the core PROV-O types, represented as structs with fields like `id`, timestamps, and relationships.
  - Expanded types like `Collection` and `Person` build on core types using composition (e.g., `Person` contains an `Agent`).
- Enums and Relationships: 
  - Relationships like `WasDerivedFrom` are modeled as structs (e.g., `Derivation`) with fields linking entities, activities, or agents.
  - Rust's `type` alias is used to match PROV-O terminology (e.g., `type WasDerivedFrom = Derivation`).
- Memory Safety: 
  - `Arc` (Atomic Reference Counting) is used for shared references (e.g., `was_generated_by: Option<Arc<Activity>>`), allowing multiple structs to reference the same instance without ownership issues.
- Optional Fields: 
    - Rust's Option is used for fields that may not always be present (e.g., generated_at_time: Option<DateTime<chrono::Utc>>).
- Collections: 
  - `Vec` is used for lists, such as `used: Vec<Arc<Entity>> in Activity`.
- Core Types:
  - `Entity`: Represents things with provenance, like a document or post. It tracks when it was generated, who created it, and what it came from.
  - `Activity`: Represents processes, like writing or editing, with start/end times and associated entities/agents.
  - `Agent`: Represents entities responsible for actions, like people or software.
- Expanded Types
  - `Collection`: An `Entity` that contains other entities (e.g., a list of posts).
  - `Person`: A specific type of `Agent` with a name.
- Relationships
  - `WasDerivedFrom`: Captures how one entity (e.g., a repost) is derived from another (e.g., an original post), optionally tied to an activity.

## Example

The `main` function demonstrates creating:

- An agent (`Alice`),
- An activity (`writing a post`),
- An original post and a repost,
- A derivation relationship between the post and repost.

## How to Run
Ensure you have Rust installed (rustc and cargo).
Add the chrono crate to your Cargo.toml:

```toml
[dependencies]
chrono = "0.4"
```

Copy the code into a provo.rs file and run it with cargo run.

This implementation provides a foundation for tracking provenance in Rust applications, such as logging data transformations or user actions, while ensuring type safety and memory efficiency.
