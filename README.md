# Detect LRRK2-G2019S protein mutation in Parkinson Disease
# Download the protein sequence LRRK2 from UniProt
# The 2019th amino acid (index 2018) is a 'G' when the protein is normal, and an 'S' when it's mutated
import tkinter
import tkinter.simpledialog 

def change_sequence(seq):
# Convert the sequence string to a list to allow mutation
    seq = list(seq)
    seq[2018] = 'S'  # Indexing starts from 0, so 2018 corresponds to the 2019th position
    seq = ''.join(seq)  # Convert the list back to a string
    return seq

def clean_sequence(seq):
# Remove newline characters from the sequence if present
    if "\n" in seq:
        seq = seq.replace("\n", "")
    return seq

def check_sequence(seq):
# Check if the sequence is long enough to include the 2019th amino acid
    if len(seq) < 2019:
        tkinter.messagebox.showinfo('Result', 'Sequence is too short')

# Check each character in the sequence to ensure it is a valid amino acid
# Valid amino acids: A, C, D, E, F, G, H, I, K, L, M, N, P, Q, R, S, T, V, W, Y
    for i in seq:
        if i not in 'ACDEFGHIKLMNPQRSTVWY':
            tkinter.messagebox.showinfo('Result', 'Invalid character in sequence')

# Ensure the entire sequence is in uppercase
    if seq != seq.upper():
        tkinter.messagebox.showinfo('Result', 'Sequence is not uppercase')

    return True

def check_mutation_G2019S(seq):
# Check the amino acid at position 2019 (index 2018)
    if seq[2018] == 'G':
        tkinter.messagebox.showinfo('Result', 'No mutation detected')  # Glycine (G) present: no mutation
    elif seq[2018] == 'S':
        tkinter.messagebox.showinfo('Result', 'G2019S Mutation detected')  # Serine (S) present: G2019S mutation
    else:
        tkinter.messagebox.showinfo('Result', 'Invalid amino acid at position 2019')  # Other amino acid: invalid

def main():
# Initialize a hidden tkinter window to use dialog boxes
    root = tkinter.Tk()
    root.withdraw()  # Hide the main tkinter window

# Prompt user to input the LRRK2 protein sequence
    seq = tkinter.simpledialog.askstring('LRRK2 Mutation', 'Enter LRRK2 protein sequence')

    # Clean the input sequence by removing newline characters
    seq = clean_sequence(seq)

# Validate the sequence
    check_sequence(seq)

# Check for G2019S mutation in the validated sequence
    check_mutation_G2019S(seq)

# Execute the main function if the script is run directly
if __name__ == "__main__":
    main()
