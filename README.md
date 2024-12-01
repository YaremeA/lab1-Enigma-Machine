# lab1-Enigma-Machine
Lab work №1 Enigma Machine

def caesar_shift(text, shift):
    return ''.join(chr((ord(char) - ord('A') + shift + i) % 26 + ord('A')) for i, char in enumerate(text))

def rotor_substitution(text, rotor):
    return ''.join(rotor[ord(char) - ord('A')] for char in text)

def rotor_reverse_substitution(text, rotor):
    reverse_rotor = {rotor[i]: chr(i + ord('A')) for i in range(26)}
    return ''.join(reverse_rotor[char] for char in text)

def enigma_machine(action, shift, rotor1, rotor2, rotor3, message):
    if action == "ENCODE":
        message = caesar_shift(message, shift)
        for rotor in (rotor1, rotor2, rotor3):
            message = rotor_substitution(message, rotor)
    elif action == "DECODE":
        for rotor in (rotor3, rotor2, rotor1):
            message = rotor_reverse_substitution(message, rotor)
        message = ''.join(chr((ord(char) - ord('A') - shift - i + 26) % 26 + ord('A')) for i, char in enumerate(message))
    return message

action = input().strip()
shift = int(input().strip())
rotor1 = input().strip()
rotor2 = input().strip()
rotor3 = input().strip()
message = input().strip()

result = enigma_machine(action, shift, rotor1, rotor2, rotor3, message)
print(result)

