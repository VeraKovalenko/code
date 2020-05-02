import os

def main() :
	s = []
	header = []
	refname = []
	ref = []
	LN = []

	print("Enter path to the .sam file (in quotes for python version older 3): ")
	path = input()
#	print path
	file = open( path, "r" )
	
	for line in file :
		s.append(list(line.split()))

	
	i = 0
	while s[i][0] != '@SQ' :
		i += 1
	while s[i][0] == '@SQ' :
		refname.append( s[i][1][3:] )
		ref.append([])
		LN.append( s[i][2][3:] )
		i += 1
	numnames = len(refname)

	while s[0][0][0] == '@' :
		header.append(s[0])
		s.pop(0)

	for line in s :
		line[3] = int(line[3])

	print("POS formated to int")

	i = 0
	while i < numnames :
		for line in s :
			if line[2] == refname[i] :
				ref[i].append(line)
		i += 1

	print("splited by refs")

	i = 0
	while i < numnames :
		ref[i].sort(key= lambda line: line[3])
		i += 1

	print("sorted")

	if len(header[0]) < 3 :
		header[0].append("SO:coordinate")
	elif header[0][2][:3] == "SO:" :
		header[0][2] = "SO:coordinate"
	else :
		header[0].insert(2, "SO:coordinate")

	outpath = path[:-4] + "_sortpy.sam"
	outfile = open( outpath, "w" )

	for line in s :
		line[3] = str(line[3])

	for line in header :
		outfile.write('\t'.join(line)+'\n')
	i = 0
	while i < numnames :
		for line in ref[i] :
			outfile.write('\t'.join(line)+'\n')
		i += 1

	outfile.close()
	file.close()
	
	print ("Complete!")
	print ("Path to the sorted file: ", outpath)

if __name__ == "__main__":
    main()
