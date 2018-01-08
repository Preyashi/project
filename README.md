# project
Network and Distributed Systems Project- Sem1

---------------------------------------------------------------------------------------------------------------------------------------
The project is as follow:
Write a program to achieve the following. Let A, B, C be three nodes. Nodes B and C get a public key certificate about their public key from node A. Then they use the public key certificate to establish a shared key between them. Nodes B and C would give the following information to node A, which would issue the public key certificate to them after verification through other channel like mobile number and e-mail. In the assignment, you do not need to do these verifications. However, note that node A still needs to verify that the sender indeed has the corresponding private key. You can only use 512-bit integer as in case of assignment 3. You can assume that the public key of node A is known.
(i) Name of the user(In reality as recorded for mobile number or Aadhar card or NIN)
(ii) Mobile number
(iii) E-mail address
(iv) Aadhar number or any other national identification number
(v) Diffie-Hellman or RSA public key
(vi) Type of public key
(vii) Public key parameters
(viii) Other functions such as hash function used in the public key certificate

----------------------------------------------------------------------------------------------------------------------------------------

Run the program
1) g++ -o a nodeA.cpp BigInteger.cc BigIntegerAlgorithms.cc BigIntegerUtils.cc BigUnsigned.cc BigUnsignedInABase.cc &> aout
2) g++ -o b nodeB.cpp BigInteger.cc BigIntegerAlgorithms.cc BigIntegerUtils.cc BigUnsigned.cc BigUnsignedInABase.cc &> bout
3) g++ -o c nodeC.cpp BigInteger.cc BigIntegerAlgorithms.cc BigIntegerUtils.cc BigUnsigned.cc BigUnsignedInABase.cc &> bout

---------------------------------------------------------------------------------------------------------------------------------------

Getting public key certified
1) B -> A : Name, details, PUB 
2) A -> B : EPUB(nonce1) 
3) B -> A : EPUA(nonce1) 
4) A -> B : EPRA(IDB, PKCB etc.)

1) C -> A : Name, details, PUC
2) A -> C : EPUC(nonce2)
3) C -> A : EPUA(nonce2)
4) A -> C : EPRA(IDC, PKCC etc.)
ID = Aadhar number
details = [Name of the user, Mobile number, E-mail address, Aadhar number, RSA public key, Public key parameters, hash function]

Public-Key Cryptography using RSA
PUB = public key of B
PUC = public key of C
PUA = public key of A
PRB = private key of B
PRC = private key of C
PRA = private key of A
PKC = [AES128(ID,Hash-SHA512(ID)), PRA(AES128 key), etc.]
PKCB = public key certificate of B issued by A
PKCC = public key certificate of C issued by A
5) B -> C : IDB, PKCB (Verification of PKCB using PUA)
6) C -> B : IDC, PKCC (Verification of PKCC using PUA)
7) C -> B : EPUB(nonce3) (Decryption using PRB)
8) B -> C : EPUC(nonce3)
9) B -> C : EPUC(nonce4) (Decryption using PRC)
10) C -> B : EPUB(nonce4)
Diffie-Hillman
11) B -> C : EPUC((g^a)modp) (Decryption using PRC)
12) C -> B : EPUB((g^b)modp) (Decryption using PRB)
Shared Key established = (g^(ab))modp

