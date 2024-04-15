import numpy as np

class CandidateElimination:
    def __init__(self, num_features):
        self.num_features = num_features
        self.S = [np.array(['0']*num_features)]  # Initialize specific boundary
        self.G = [np.array(['?']*num_features)]  # Initialize general boundary

    def is_consistent(self, instance, hypothesis):
        for i in range(len(hypothesis)):
            if hypothesis[i] != '?' and hypothesis[i] != instance[i]:
                return False
        return True

    def eliminate(self, instance, label):
        if label == 'Y':  # Positive instance
            self.G = [g for g in self.G if self.is_consistent(instance, g)]
            for s in list(self.S):
                if not self.is_consistent(instance, s):
                    self.S.remove(s)
                    for i in range(len(s)):
                        if s[i] != instance[i]:
                            new_s = np.copy(s)
                            new_s[i] = '?'
                            self.S.append(new_s)
        else:  # Negative instance
            self.S = [s for s in self.S if self.is_consistent(instance, s)]
            for g in list(self.G):
                if not self.is_consistent(instance, g):
                    self.G.remove(g)
                    for i in range(len(g)):
                        if g[i] != instance[i] and self.S[0][i] == '?':
                            new_g = np.copy(g)
                            new_g[i] = self.S[0][i]
                            self.G.append(new_g)

    def print_hypotheses(self):
        print("Specific boundary (S):", self.S)
        print("General boundary (G):", self.G)


# Example usage:
# Assume the dataset has 4 features
ce = CandidateElimination(4)

# Define a dataset
data = [
    (['Sunny', 'Warm', 'Normal', 'Strong'], 'Y'),
    (['Sunny', 'Warm', 'High', 'Strong'], 'Y'),
    (['Rainy', 'Cold', 'High', 'Strong'], 'N'),
    (['Sunny', 'Warm', 'High', 'Strong'], 'Y'),
]

# Train the algorithm
for instance, label in data:
    ce.eliminate(instance, label)

# Print the hypotheses
ce.print_hypotheses()
