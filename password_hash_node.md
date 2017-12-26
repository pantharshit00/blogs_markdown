Password hashing is an important part of data integrity and security when storing sensitive data in the database. One should simply should not store raw passwords in the database. There are many libraries for password hashing like bcrypt, pbkdf2 and argon2. In this blog post we are going to implement password hashing using the default encryption library which come along with node.js this is crypto. We are going to use [Password Based Key Derivative Function 2](https://en.wikipedia.org/wiki/PBKDF2) (pbkdf2) as the algorithm to hash our password. This function is provided by the crypto library.

<hr>

## What is Password Hashing

Before writing some code I'd like to talk briefly about password hashing._A hash function is any function that can be used to map data of arbitrary size to data of fixed size_(Taken from Wikipedia). That means hash is a secure representation of a string. It is a one way function. One cant simply get the original string back from the hash string. The string resolve to the same hash if passed through the same hash function each time even infinity times. But this caused a caveat though. To breach hash hackers may use a [rainbow table](https://en.wikipedia.org/wiki/Rainbow_table). Rainbow tables contains hashes of commonly string say string 123456789. So to overcome this problem we add a _salt_ which can be a random string in the original string. Like we may add 5d6sde to 123465789 it becomes 5d6sde123456789 before hashing. So it is certainly impossible any rainbow table in world will contain hash for this string. To be even more secure certain password hashing functions provide way to hash the generated hash a certain number of iteration. So this way the hash will be impossibe to decrypt.

<hr>

## Lets Code a Hashing system using crypto library

<script src="https://embed.runkit.com" data-element-id="code"></script>

<div id="code" style="height:100%;width:100%">
const crypto = require('crypto');
// Create password hash using Password based key derivative function 2
function hashPassword(password) {
    const salt = crypto.randomBytes(16).toString('hex');
    const hash = crypto.pbkdf2Sync(password, salt, 2048, 32, 'sha512').toString('hex');
    return [salt, hash].join('$');
}

// Checking the password hash
function verifyHash(password, original) {
const originalHash = original.split('$')[1];
const salt = original.split('$')[0];

    const hash = crypto.pbkdf2Sync(password, salt, 2048, 32, 'sha512').toString('hex');

    if (hash === originalHash)
        return true;
    else
        return false;

}

let hash = hashPassword('test');
console.log('HASH = '+hash);
console.log(verifyHash('test',hash));
console.log(verifyHash('test1',hash));

</div>
