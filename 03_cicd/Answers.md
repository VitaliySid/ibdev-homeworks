### Результаты выполнения

Отправьте в личном кабинете студента найденные вами секреты с описанием того, чтобы это могло быть по вашему мнению.
1. Тут вероятно представлена миграция БД сервиса, где добавляются два пользователя с одинаковым паролем.
Отображены их логины и роли.  
Хеш пароля `$2a$10$ctPFhgJh.YIE21AA0OGl5er3p9f3XsAwkmTXnP2I7BxCpQbr1QAg2` 
выглядит как `bcrypt $2*$, Blowfish (Unix)`  
```
    Reason: High Entropy
    Date: 2021-01-21 07:06:57
    Hash: 357116ea59d9d0d4cfe8bed75c09da0f3ee99b2a
    Filepath: service/docker-entrypoint-initdb.d/01_data.sql
    Branch: origin/master
    Commit: feat(service): symmetric version added

    @@ -1,4 +0,0 @@
    -INSERT INTO users(login, password, roles)
    -VALUES
    -       ('admin', '$2a$10$ctPFhgJh.YIE21AA0OGl5er3p9f3XsAwkmTXnP2I7BxCpQbr1QAg2', '{"ADMIN", "USER"}'), -- у этого пользователя две роли (т.е. он и админ, и обычный юзер)
    -       ('user', '$2a$10$ctPFhgJh.YIE21AA0OGl5er3p9f3XsAwkmTXnP2I7BxCpQbr1QAg2', '{"USER"}');
```

2. Два коммита с добавлением и удалением закрытого, открытого и симметричного ключа, которые использовались для генерации пароля и JWT токенов. В дальнейшем ключи заменили на скрипты генерации ключей.  

Закрытый ключ:  
```
    Reason: High Entropy
    Date: 2021-01-21 07:06:57
    Hash: 357116ea59d9d0d4cfe8bed75c09da0f3ee99b2a
    Filepath: service/keys/private.key
    Branch: origin/master
    Commit: feat(service): symmetric version added

    @@ -1,27 +0,0 @@
    ------BEGIN RSA PRIVATE KEY-----
    -MIIEpAIBAAKCAQEAxFv8lbJ+njQ1thnz25qZAsEQB0yRhz+Ri3X9r9+6M97dus80
    -BRdkRaQPHxJxNaAKQc1HylYqBITS3mMSGjwsJ6WtlIAoR8PBUY8fnidjVagTkLFO
    -dzZ+rEEOJtRB0zLUmeDxxDg2qMan2ijn2nksAshRhJQ8eNc84cdZ0pPdKz3ay774
    -Ccj3gHcYHmadICs6nIjcVuJ9S1z16sT7LBiOWR6hlVeV/lJ+1TYrhiTPW+j7CZaX
    -w/BbQZ+mKi/6QpY39tQntz73WIlqGO6uhLxpgUtFI+aZrcLXTHSWiSJLs9KAx++Q
    -5KMF86NOPu8poA+f1twa3jN1NM/lQQBwKhmXbQIDAQABAoIBAQCKbC5LeWE5NaUH
    -kpQOI5XqEx+xhZCxv2Zi4fLMoPMqzdmRb7BERpExZs4iIWYdX4zbhlMtmEBWnyvo
    -Cf8g73pRGMKdBRtgO+d0D2lCnJGyOKJSRiwCbjAuTk4joU4mDJdDQwgsQ1SE9kYt
    -zNhlczZLX9vXkohux4zrvRTdFc+8QsoojlKwRTpRUFoJW7V5yfU9BqrujTqhWdDm
    -m8VlcvWgPsX5djyDamgZuGr7aKjAMI4bXGahBIQdkWnpRnGu5e1gM1tCOqt/0WiR
    -iTRkew0P6tyLqaCzlTheOEOGil74d8IANfOBO3ePqObuGBuBtsFzr9OgJ7MreXH0
    -03CAsfUhAoGBAOpLN7hMNpw2wQp3DLXt9sn5MTyffEYVjK9IWeDErZNIDCKFXgwD
    -mwstTBSIXA0ORPs5YGJJ+ZbvRUnWsViMvT9tyKu365hrFTpDl28boXdSVSQ7D3ig
    -NmTF6HG5Yg+0v3cQD/dDcoi3YlJY7Bnw9KNMv6xemwzuq5A4Xv5RTndjAoGBANaN
    -Eh0gmmj+YaHhY+2MjO0TQFn1PMLxbwFvPJ/IfxbMg+ZZAXDV7fT8LlSWY4hnp44W
    -dZadlkdNZt1Dqs+xuiN0yE6HeLVa9rB1tpxhneKm3y+L2SThc+laQl7jnzkZaa//
    -HEQURfCmmLgJTZ0gtUc4Z9bN/rNC1gRdUD+wFfbvAoGBANqyN2KqkVcjrPGNyqmP
    -ZIuHNbR20lPBDb8X8/1g2PzfhaQ7hVwFiZXXRGruFa6CIVW3awaUMov28GBKLOSR
    -Cp3IZkYTubBeVEQ8j4BA9GkiyyK0lm5sbhmGusBc4PH0L7x9m8mcha6kLvza0Bgu
    -2MwNeeT1shlSN4a5d8JANtQtAoGAH09fAVksr33QCau2xYfpWP+iOH6Na3WIWZE+
    -K6M6yLz30rnSeAEAROw4Zqe7xsA5t4aXim9c6vLkvA2P89df7qSwRqWGfBDWR1Im
    -YBPu0pC/qVSjT7qHC9rcLLTTG6YVwlVcbqL2wfPN/a194hxP2CDnJnXRYZ+zU9e6
    -SlEMI4kCgYBa11Nlkt2YwHdpu0MAvTeA76983aQ20Tczx4qX17aOLdDdnVVQzoqr
    -tZWXbWOrRJohpU/kSJYxrcK3fFdPJ2ctwe7jqVTylEo3yfpdgLLd+5ZQRt/+4kt6
    -BTS1gNCQSJt8M2QznbIlNyWXi3jpjjKp7uyHJT/3r++5dfLmf5JE1g==
    ------END RSA PRIVATE KEY-----
```    
  
Открытый ключ:  
```
    Reason: High Entropy
    Date: 2021-01-21 07:06:57
    Hash: 357116ea59d9d0d4cfe8bed75c09da0f3ee99b2a
    Filepath: service/keys/public.key
    Branch: origin/master
    Commit: feat(service): symmetric version added

    @@ -1,9 +0,0 @@
    ------BEGIN PUBLIC KEY-----
    -MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAxFv8lbJ+njQ1thnz25qZ
    -AsEQB0yRhz+Ri3X9r9+6M97dus80BRdkRaQPHxJxNaAKQc1HylYqBITS3mMSGjws
    -J6WtlIAoR8PBUY8fnidjVagTkLFOdzZ+rEEOJtRB0zLUmeDxxDg2qMan2ijn2nks
    -AshRhJQ8eNc84cdZ0pPdKz3ay774Ccj3gHcYHmadICs6nIjcVuJ9S1z16sT7LBiO
    -WR6hlVeV/lJ+1TYrhiTPW+j7CZaXw/BbQZ+mKi/6QpY39tQntz73WIlqGO6uhLxp
    -gUtFI+aZrcLXTHSWiSJLs9KAx++Q5KMF86NOPu8poA+f1twa3jN1NM/lQQBwKhmX
    -bQIDAQAB
    ------END PUBLIC KEY-----   
```
  
Симметричный ключ:  
  
```
Reason: High Entropy
Date: 2021-01-21 07:06:57
Hash: 357116ea59d9d0d4cfe8bed75c09da0f3ee99b2a
Filepath: service/keys/symmetric.key
Branch: origin/master
Commit: feat(service): symmetric version added

@@ -1,6 +0,0 @@
-INZqU5znzA+Kzb9SltHwINpSOzu99scvH3B3YqJYSap+M8ubNQo7mYURxR3gKbnv
-TR5XJkiKBXALhC9/KlaDFGJEjo4o8xVC1lWgTwSx0p05tG+g8JMoQRCDoWz9f73+
-PEiP3Z5Z0YjlSBBr4rp/CqUK+B8PhdMddJTNT4Hli6EwXqltJXoNqAMZUrNLvm6n
-BBvJVebK2J+NqeZrsqteoWMLyAPfVa/RBrDlhhvOo4Z4O5uztulc2Kc2EMWSuquj
-D93o+I4bBnrl2oSdl0F2uky6c4UYM5xyLrryeX9alKfPn9YUKEZwA/JZuh0fAyl8
-sPcddvjdmhm6smAYhI8yKw==
```
  
После анализа другого репозитория
`trufflehog https://github.com/netology-code/ib-secrets-fixed.git | tee -a log1.txt`  
   
Ключи были удалены из истории, но скрипты миграций БД из п.1. остались.
