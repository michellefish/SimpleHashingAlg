SimpleHashingAlg
================

COMP 5370 Fall 2012
Implement the following simple hashing algorithm:

The program should hash the file specified in the first argument when called. If no arguments are given, it should read from stdin and hash the user's input

	input <- "string to be hashed"
	key <- "Hamilton's awesome hash function"

	//pad input to ensure the length is a multiple of 32. this will append the necessary number of bytes from the beginning of the key
	if length(input) == 0 || length(input) % 32:
		input += key[:32-length(input)%32]

	hash <- key
	for block_32 in input: //break input into 32-byte blocks
		hash <- hash xor block_32
		if hash[0] % 2:
			for i in [0, 32):
				//increment each byte by 42 (modulo 256)
				hash[i] <- (hash[i] + 42) % 256
		if hash[1] % 3:
			//move the first 10 bytes to the end
			hash <- hash[10:] + hash[:10]
	
	//your hash may contain non-printable characters, so make sure you hex encode it
	print hex(hash)


TEST CASES
"" (empty string)	0000000000000000000000000000000000000000000000000000000000000000
"foo"			4e460445121808164f0504530041151d4e0501070c1a2e0e02210d190602531c
"Drew Hamilton"		540e192d1202040954070f541b0007020b101b040a4e0c13081e4c3c0e034e1f
