# Detect-LRRK2-G2019S-protein-mutation-in-Parkinson-Disease
import tkinter
import tkinter.simpledialog

def change_sequence(seq):
# Replace the 2019th amino acid with a S
    seq = list(seq)
    seq[2018] = 'S'
    seq = ''.join(seq)
    return seq

def clean_sequence(seq):
# If sequence has a \n character remove it
    if "\n" in seq:
        seq = seq.replace("\n", "")
    
    return seq

def check_sequence(seq):
    if len(seq) < 2019:
        tkinter.messagebox.showinfo('Result', 'Sequence is too short')
    
# Check if the characters in the sequence are valid, if the character is not A C D E F G H I K L M N P Q R S T V W Y
# raise a ValueError
    for i in seq:
        if i not in 'ACDEFGHIKLMNPQRSTVWY':
            tkinter.messagebox.showinfo('Result', 'Invalid character in sequence')
    
# Check if all the characters in the sequence are uppercase, if not raise a ValueError
    if seq != seq.upper():
        tkinter.messagebox.showinfo('Result', 'Sequence is not uppercase')
    
    return True

def check_mutation_G2019S(seq):
    if seq[2018] == 'G':
        tkinter.messagebox.showinfo('Result', 'No mutation detected')
    elif seq[2018] == 'S':
        tkinter.messagebox.showinfo('Result', 'G2019S Mutation detected')
    else:
        tkinter.messagebox.showinfo('Result', 'Invalid amino acid at position 2019')

def main():
# Write a sequence in a dialog box and check if it is valid
    root = tkinter.Tk()
    root.withdraw()
    seq = tkinter.simpledialog.askstring('LRRK2 Mutation', 'Enter LRRK2 protein sequence')
    seq = clean_sequence(seq)
    check_sequence(seq)
    check_mutation_G2019S(seq)

if __name__ == "__main__":
    main()
