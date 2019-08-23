### xodus
---
https://jetbrains.github.io/xodus/

```java
try (Environment env = Environments.newInstance("/home/me/.myAppData")) {
  env.executeInTransaction(txn -> {
    final Store store = env.openStore("Messages", StoreConfig.WITHOUT_DUPLICATES, txn);
    store.put(txn, StringBing.stringToEntry("Hello"), StringBinding.stringToEntry("World!"));
  });
}


try (PersistentEntityStore entityStore = PersistentEntityStores.newInstance("/home/me/.myAppData")) {
  entityStore.executeInTransaction(txn -> {
    final Entity message = txn.newEntity("Message");
    message.setProperty("hello", "World!");
  });
}

try (Environment env = Environments.newInstance("/home/me/.myAppData")) {
  final VirtualFileSystem vfs = new VirtualFileSystem(env);
  env.executeInTransaction(txn -> {
    final File file = vfs.createFile(txn, "Messages");
    try (DataOutputStream output = new DataOutputStream(vfs.writeFile(txn, file))) {
      output.writeUTF("Hello ");
      output.writeUTF("World!");
    } catch (IOException e) {
      throw new ExodusException(e);
    }
  });
  vfs.shutdown();
}
```

```sh
./gradlew build
./gradlew assemble
```

```
```


