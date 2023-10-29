# cyberDemo
cyber github
"""
Author: Or Geller
Description:
for parameter encrypt - encrypts an input and saves in file
for parameter decrypt - decrypts a file content and prints it
"""
import sys


encryption_table = {
        'A': '56', 'B': '57', 'C': '58', 'D': '59', 'E': '40', 'F': '41', 'G': '42', 'H': '43', "I": '44', "J": '45',
        "K": '46', "L": '47', "M": '48', "N": '49', "O": '60', "P": '61', "Q": '62', "R": '63', "S": '64', "T": '65',
        "U": '66', "V": '67', "W": '68', "X": '69', "Y": '10', "Z": '11', "a": '12', "b": '13', "c": '14', "d": '15',
        "e": '16', "f": '17', "g": '18', "h": '19', "i": '30', "j": '31', "k": '32', "l": '33', "m": '34', "n": '35',
        "o": '36', "p": '37', "q": '38', "r": '39', "s": '90', "t": '91', "u": '92', "v": '93', "w": '94', "x": '95',
        "y": '96', "z": '97', " ": '98', ",": '99', ".": '100', ";": '101', "'": '102', "?": '103', "!": '104',
        ":": '105'
}

decryption_table = {value: key for key, value in encryption_table.items()}


def encrypt(message):
    encrypted_message = []
    for char in message:
        if char in encryption_table:
            encrypted_message.append(encryption_table[char])
    return ','.join(encrypted_message)


def decrypt(encrypted_message):
    decrypted_message = ''
    encrypted_chars = encrypted_message.split(',')
    for char_code in encrypted_chars:
        if char_code in decryption_table:
            decrypted_message += decryption_table[char_code]
    return decrypted_message


def main():
    if len(sys.argv) != 2:
        print("wrong data input, input encrypt/decrypt")
        print(sys.argv)
        return

    operation = sys.argv[1]

    if operation == 'encrypt':
        message = input("Enter a message to encrypt: ")
        encrypted_message = encrypt(message)
        with open("encrypted_msg.txt", 'w') as file:
            file.write(encrypted_message)
        print(f"Encrypted message saved in 'encrypted_msg.txt'")
    elif operation == 'decrypt':
        with open("encrypted_msg.txt", 'r') as file:
            encrypted_message = file.read()
        decrypted_message = decrypt(encrypted_message)
        print(f"Decrypted message: {decrypted_message}")
    else:
        print("Invalid operation. Use 'encrypt' or 'decrypt'.")


if __name__ == '__main__':
    main()
