# Amazon S3 Object Versioning

![Image](https://github.com/user-attachments/assets/51b25ac5-a285-43ab-9acb-7d6bd69908f6)

Amazon S3 Object Versioning is a powerful feature that allows you to preserve, retrieve, and restore every version of every object in a bucket. This ensures that you can recover from accidental deletions, overwrites, or other unintended changes.


## Key Concepts of S3 Versioning

Enabling Versioning

- Versioning is enabled at the bucket level.

- Once enabled, it cannot be turned off—only suspended.

- When versioning is suspended, new objects are stored as null versions.


## How Versioning Works

![Image](https://github.com/user-attachments/assets/f0a30300-e737-445c-990b-8351822fad90)

- Each time an object is modified (e.g., uploaded, deleted, or overwritten), S3 creates a new version of the object.

- Each version has a unique version ID assigned by S3.

- All versions of an object are stored in the same bucket, and you are billed for the storage of all versions.



## Behavior of Versioning

### Uploading an Object

![Image](https://github.com/user-attachments/assets/6f37172d-46ff-42bb-850d-ca8a8212fa4a)

When you upload an object to a versioned bucket:

- If the object does not already exist, S3 creates a new object with a unique version ID.

- If the object already exists, S3 creates a new version of the object with a new version ID. The older version is retained.

Example:

Upload winkie.jpg (Version ID: 111111).

Upload winkie.jpg again (Version ID: 222222).

Both versions (111111 and 222222) are stored in the bucket.


### Deleting an Object

![Image](https://github.com/user-attachments/assets/7dbf1a2a-c7b0-4e3c-868b-c148bd1fe365)

When you delete an object in a versioned bucket:

- S3 does not actually delete the object. Instead, it adds a delete marker to the object.

- The delete marker becomes the current version of the object, making it appear as if the object is deleted.

- The previous versions of the object remain intact and can be restored.

Example:

Delete winky.jpg (Version ID: 222222).

S3 adds a delete marker (Version ID: 333333).

The object appears deleted, but the previous versions (111111 and 222222) are still stored.


### Restoring a Deleted Object

To restore a deleted object:

- Delete the delete marker.

- The previous version of the object becomes the current version again.

Example:

Delete the delete marker (333333).

The previous version (222222) becomes the current version, and the object is restored.


### Overwriting an Object

![Image](https://github.com/user-attachments/assets/6f37172d-46ff-42bb-850d-ca8a8212fa4a)

When you upload an object with the same name as an existing object:

- S3 creates a new version of the object.

- The older version is retained.

Example:

Upload winkie (Version ID: 444444).

The previous version (222222) is retained.


### Suspending Versioning

![Image](https://github.com/user-attachments/assets/9880194e-444f-42e4-8b0b-c72e82f690e5)

When versioning is suspended:

- New objects are stored as null versions.

- Existing versions are preserved.

- Uploading an object with the same name overwrites the current version (no new version is created).

Example:

Suspend versioning.

Upload winkie (Version ID: null).

The previous winkie (444444) is retained, but no new version is created.


## Use Cases for Versioning

Accidental Deletion Protection:

- Restore objects if they are accidentally deleted.

Data Recovery:

- Recover from unintended overwrites or modifications.

Audit and Compliance:

- Maintain a history of object changes for compliance purposes.

Rollback:

- Revert to a previous version of an object if needed.


## Conclusion

Amazon S3 Object Versioning is a robust feature for protecting your data from accidental deletions, overwrites, and other unintended changes. By understanding how versioning works—including uploads, deletions, and restorations—you can effectively manage your S3 objects and ensure data durability. However, be mindful of the storage costs associated with maintaining multiple versions, and use lifecycle policies to optimize costs.




