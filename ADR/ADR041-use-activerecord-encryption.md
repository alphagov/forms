# ADR041: Use ActiveRecord encryption in Runner

Date: 2025-02-12

## Status

Accepted

## Context

Runner will be storing user submitted data which is likely to include sensitive information, such as PII including document IDs like passport numbers.

Aurora RDS databases will already encrypt when data is saved to disk with AWS KMS, but while data is held in memory it is not. To mitigate against this we can additionally encrypt at the application level, so data is not stored in the database in plain text. Though a low risk, accidental leakage is doubly assured against having that sensitive user information exposed.

Rails makes this quite easy to do with [ActiveRecord Encryption](https://guides.rubyonrails.org/active_record_encryption.html).

### Pros

* If there is more access to credentials to query data in the database than there is to your encryption keys. For example, if we allowed devs with the support role in AWS to query the database, we might want to make sure they don’t have access to user submission data. However, if we decide to do this in the future we can start encrypting the data later, as Active Record encryptions supports reading unencrypted data when encryption has been enabled.
* If sensitive data is leaked, for example in the SQL logs, it's encrypted and unreadable.
* An additional layer of defence from an accidental information disclosure by our engineers who have access to the database. Instances such as an engineer being able to read the plaintext entries while querying the database, or that information being accidentally saved to logs or out to monitoring systems.
* Mitigates against leaks or modification if restrictions to our database backups is compromised, say from leaked credentials. Though it is very low likelihood that the access encryption key that has access to both the backups and the database encryption would also compromised.
* Mitigates against internal malicious actors being able to read or modify data. However we already require security clearance, so impact is minimal unless we restrict access to the keys and the app itself.
* This additional layer is something we can assure departments with so they have more confidence in using Forms.

### Cons

* Extra keys to manage, extra configuration in Rails.
* Difficulty accessing the data if we ever need to inspect it. The main reason I can see for doing this is if for some reason we fail to send a submission due to a data error and need to inspect the data itself to diagnose and fix any issues.

## Decision

Use ActiveRecord Encryption to encrypt data at the application level before it gets stored in the database. As part of implementation, we will also create an auditable and secure method to access submission data in case of incidents.

## Consequences

There will be more keys to manage. It will be harder for us to read the data. We have stronger protection against accidental leakage of data. We have better assurance for our users.
