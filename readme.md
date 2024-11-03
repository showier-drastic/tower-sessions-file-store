# Usage

```rs
let session_store = FileSessionStorage::new();
let session_layer = SessionManagerLayer::new(session_store)
    .with_secure(false)
    .with_same_site(tower_sessions::cookie::SameSite::Lax)
    .with_name("yq_session_store_id")
    .with_expiry(Expiry::OnInactivity(Duration::days(360)));
let deletion_task = tokio::task::spawn(
    session_store
        .clone()
        .continuously_delete_expired(tokio::time::Duration::from_secs(60 * 60)),
);

app.layer(session_layer);
```

Issues or pull requests welcome.
