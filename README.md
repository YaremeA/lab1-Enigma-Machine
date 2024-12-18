# lab1-Enigma-Machine
Lab work №1 Enigma Machine
# Perform Caesar shift with an incremental step
def caesar_shift(text, shift):
    return ''.join(chr((ord(char) - ord('A') + shift + i) % 26 + ord('A')) for i, char in enumerate(text))

# Substitute characters using the rotor mapping
def rotor_substitution(text, rotor):
    return ''.join(rotor[ord(char) - ord('A')] for char in text)

# Reverse substitution using rotor mapping
def rotor_reverse_substitution(text, rotor):
    reverse_rotor = {rotor[i]: chr(i + ord('A')) for i in range(26)}
    return ''.join(reverse_rotor[char] for char in text)

# Simulate Enigma machine encoding or decoding
def enigma_machine(action, shift, rotor1, rotor2, rotor3, message):
    if action == "ENCODE":
        # Apply Caesar shift
        message = caesar_shift(message, shift)
        # Pass through rotors
        for rotor in (rotor1, rotor2, rotor3):
            message = rotor_substitution(message, rotor)
    elif action == "DECODE":
        # Reverse through rotors
        for rotor in (rotor3, rotor2, rotor1):
            message = rotor_reverse_substitution(message, rotor)
        # Reverse Caesar shift
        message = ''.join(chr((ord(char) - ord('A') - shift - i + 26) % 26 + ord('A')) for i, char in enumerate(message))
    return message

# Read inputs
action = input().strip()  # ENCODE or DECODE
shift = int(input().strip())  # Initial Caesar shift value
rotor1 = input().strip()  # Rotor 1 substitution mapping
rotor2 = input().strip()  # Rotor 2 substitution mapping
rotor3 = input().strip()  # Rotor 3 substitution mapping
message = input().strip()  # Message to process

# Perform Enigma machine processing
result = enigma_machine(action, shift, rotor1, rotor2, rotor3, message)

# Print the result
print(result)


