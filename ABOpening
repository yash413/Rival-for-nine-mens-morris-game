positions_evaluated = 0

# Static estimation function
# Calculates the static estimate value of the board position when the leaf nodes are reached
# Input: Board position is given as the input
# Output: A value is returned for the given board position
def static_estimation(b):
    global positions_evaluated
    positions_evaluated += 1
    numWhitePieces = 0
    numBlackPieces = 0
    for i in b:
        if i == "W":
            numWhitePieces += 1
        elif i == "B":
            numBlackPieces += 1
    return numWhitePieces - numBlackPieces

# closeMill function 
# To check if the current move makes a mill
# Input: a location j in the array representing the board and the board b
# Output: returns True if the move to j closes a mill or else returns False
def closeMill(j, b):
    C = b[j]

    def zero():
        if (b[2] == b[4] == C):
            return True
        else:
            return False

    def one():
        if (b[3] == b[5] == C) or (b[8] == b[17] == C):
            return True
        else:
            return False

    def two():
        if (b[0] == b[4] == C):
            return True
        else:
            return False

    def three():
        if (b[1] == b[5] == C) or (b[7] == b[14] == C):
            return True
        else:
            return False

    def four():
        if (b[0] == b[2] == C):
            return True
        else:
            return False

    def five():
        if (b[1] == b[3] == C) or (b[6] == b[11] == C):
            return True
        else:
            return False

    def six():
        if (b[5] == b[11] == C) or (b[7] == b[8] == C):
            return True
        else:
            return False

    def seven():
        if (b[3] == b[14] == C) or (b[6] == b[8] == C):
            return True
        else:
            return False

    def eight():
        if (b[6] == b[7] == C) or (b[1] == b[17] == C):
            return True
        else:
            return False

    def nine():
        if (b[10] == b[11] == C) or (b[12] == b[15] == C):
            return True
        else:
            return False

    def ten():
        if (b[9] == b[11] == C) or (b[13] == b[16] == C):
            return True
        else:
            return False

    def eleven():
        if (b[5] == b[6] == C) or (b[9] == b[10] == C) or (b[14] == b[17] == C):
            return True
        else:
            return False

    def twelve():
        if (b[9] == b[15] == C) or (b[13] == b[14] == C):
            return True
        else:
            return False

    def thirteen():
        if (b[12] == b[14] == C) or (b[10] == b[16] == C):
            return True
        else:
            return False

    def fourteen():
        if (b[3] == b[7] == C) or (b[12] == b[13] == C) or (b[11] == b[17] == C):
            return True
        else:
            return False

    def fifteen():
        if (b[16] == b[17] == C) or (b[12] == b[9] == C):
            return True
        else:
            return False

    def sixteen():
        if (b[15] == b[17] == C) or (b[13] == b[10] == C):
            return True
        else:
            return False

    def seventeen():
        if (b[1] == b[8] == C) or (b[15] == b[16] == C) or (b[14] == b[11] == C):
            return True
        else:
            return False

    switch = {0: zero, 1: one, 2: two, 3: three, 4: four, 5: five,
              6: six, 7: seven, 8: eight, 9: nine, 10: ten, 11: eleven,
              12: twelve, 13: thirteen, 14: fourteen, 15: fifteen, 16: sixteen, 17: seventeen}

    return switch[j]()

# generateRemove function
# Removes the Blackpieces from the given board which are not in the mill and adds that position to the list
# Input: a board position and a list L
# Output: positions are added to L by removing black pieces
# If no blackpieces can be removed the given board is added to the list
def generateRemove(b, L):
    a1 = len(L)
    for i in range(len(b)):
        if b[i] == "B":
            if not closeMill(i, b):
                b1 = b[:]
                b1[i] = 'x'
                L.append(b1)
    a2 = len(L)
    if a1 == a2:
        L.append(b)

# GenerateAdd function
# adds a whitepiece in available places and adds that position to the list
# Input: a board position
# Output: a list L of board positions
def GenerateAdd(b):
    L = []
    for i in range(len(b)):
        if b[i] == 'x':
            b1 = b[:]
            b1[i] = 'W'
            if closeMill(i, b1):
                generateRemove(b1, L)
            else:
                L.append(b1)
    return L

# WtB function
# Converts all the whitepieces to black and blackpieces to white
# Input: a board position
# Output: a board position where all the whites are swapped to black and vice-versa
def WtB(b):
    b1 = b[:]
    for i in range(len(b1)):
        if b1[i] == "W":
            b1[i] = "B"
        elif b1[i] == "B":
            b1[i] = "W"
    return b1

# leaf function
# Checks if the given board posiition is a leaf
# Input: a board position
# Output: returns True if the given board position is a leaf or else returns False
def leaf(b):
    numWhitepieces = 0
    numBlackpieces = 0
    for i in b:
        if i == 'W':
            numWhitepieces += 1
        elif i == 'B':
            numBlackpieces += 1
    if (numWhitepieces == 8 or numBlackpieces == 8):
        return True
    else:
        return False

# MinMax_alb function
# Generates the moves for the current min node position and returns the minimum value for all the generated moves based on static estimation value
# Input: a board position, depth of the current node posiition, alpha and beta values
# Output: Generates the min node moves for the current board position by swapping the blacks and whites using WtB function 
#         and compares the current minimum value with MaxMin_alb value of all generated moves and returns the minimum value.
def MinMax_alb(b, ply, al, beta):
    if ply == depth:
        return static_estimation(b)
    else:
        ply += 1
        b = WtB(b)
        v = 10000
        x = GenerateAdd(b)
        for i in x:
            i = WtB(i)
            v = min(v, MaxMin_alb(i, ply, al, beta))
            if v <= al:
                return v
            else:
                beta = min(v, beta)
        return v

# MaxMin_alb function
# Generates the moves for the current max node position and returns the maximum value for all the generated moves based on static estimation value
# Input: a board position, depth of the current node posiition, alpha nad beta values
# Output: if    a leaf node or a node at the maximum depth is reached it returns the static estimation value of that board position
#         else  Generates the max node moves for the current board position and compares the current maximum value with MinMax_alb value of all 
#               generated moves and returns the maximum value. If the depth is 1, the board position for the max value is also returned.
def MaxMin_alb(b, ply, al, beta):
    if leaf(b) or ply == depth:
        return static_estimation(b)
    else:
        ply += 1
        v = -10000
        y = GenerateAdd(b)
        x = 0
        for i in y:
            m = MinMax_alb(i, ply, al, beta)
            if m > v:
                x = i
                v = m
            if v >= beta:
                if ply == 1:
                    return x, v
                else:
                    return v
            else:
                al = max(v, al)
        if ply == 1:
            if x == 0:
                x = y[0]
            return x, v
        return v

# Input of the program
(f1, f2, depth) = list(input().split())
depth = int(depth)
file1 = open(f1)
l1 = list(file1.read())
s = ""
count = 0
for i in l1:
    s += i
    if i == 'W':
        count += 1

# Checks if the given depth is 
if depth == 0:
    file2 = open(f2, "w")
    file2.write("No moves are calculated" + "\n\n" + "Board position is: " + s)

# Checks if the opening game is ended for the current player
elif count == 8:
    file2 = open(f2, "w")
    file2.write("No further moves are there" + "\n\n" + "The opening game is completed for the player" + "\n\n" + "Board position is: " + s )

# If none of the above conditions are satisfied Alpha beta pruning algorithm is executed
else:
    (A1, A2) = MaxMin_alb(l1, 0, -10000, 10000)
    s = ""
    for i in A1:
        s += i
    file2 = open(f2, "w")
    file2.write("Board position is: " + s + "\n\n" + "Positions evaluated by static estimation: " + str(positions_evaluated) + "\n\n"
                + "MINIMAX estimate: " + str(A2))
