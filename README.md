#Crack - Brute Force Password Cracking
Modern computers overwhelmingly use multi-core architectures. Exploiting this hardware for parallel programming (creating a program that executes simultaneously on more than one processor core) requires the use of multiple threads. We will use one of the most basic threading interfaces, Pthreads, to create a multi-threaded password cracking program.

In this lab, you will:

1. Use crypt() and crypt_r() to guess password hashes
2. Iterate over aribtrary length strings with characters from 'a' to 'z'
3. Create and wait for threads with pthread_create() and pthread_join()
4. Divide work between multiple parallel threads

#Usage

./crack threads keysize target

#Description

crack should attempt to find the password associated to the target DES hash. It does this by trying all possible lowercase alphabetic (a-z) passwords of length up to keysize. The program should run with threads concurrent threads for speed.

Linux/Unix user passwords are never stored on the system. Instead, a function called a hash is applied to the password. Then, the hashed password is stored, traditionally in /etc/passwd or more recently in /etc/shadow. The classic hash function on Unix systems is crypt(3). To make things harder on crackers, crypt also uses a two character string called a salt which it combines with the password to create the hash. Schematically:

password + salt => crypt() => hash

The salt is visible in the hash as the first two characters. As an example, a password 'apple' and salt 'na' become the hash 'na3C5487Wz4zw'.

The crack program should extract the salt from the first two characters of target, then repeatedly call crypt() using all possible passwords built of up to keysize lowercase alphabetic characters.

When a match to target is found, the program should print the cracked password and exit immediately. If the entire space of passwords is searched with no match, the program should exit with no output.
