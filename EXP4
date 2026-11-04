#include <iostream>
#include <queue>
#include <unordered_map>
#include <string>
using namespace std;

struct Node {
    char ch;
    int freq;
    Node *left, *right;

    Node(char c, int f) {
        ch = c;
        freq = f;
        left = right = nullptr;
    }
};

struct Compare {
    bool operator()(Node* a, Node* b) {
        return a->freq > b->freq;
    }
};

void generateCodes(Node* root, string code,
                   unordered_map<char, string>& huffmanCode) {
    if (root == nullptr)
        return;

    if (root->left == nullptr && root->right == nullptr) {
        huffmanCode[root->ch] = code;
        return;
    }

    generateCodes(root->left, code + "0", huffmanCode);
    generateCodes(root->right, code + "1", huffmanCode);
}

string decode(Node* root, const string& encoded) {
    string decoded;
    Node* current = root;

    for (char bit : encoded) {
        if (bit == '0')
            current = current->left;
        else
            current = current->right;

        if (current->left == nullptr &&
            current->right == nullptr) {
            decoded += current->ch;
            current = root;
        }
    }

    return decoded;
}

int main() {
    string text;

    cout << "Enter the text: ";
    getline(cin, text);

    if (text.empty()) {
        cout << "Text cannot be empty.\n";
        return 0;
    }

    // Frequency calculation
    unordered_map<char, int> frequency;

    for (char ch : text)
        frequency[ch]++;

    // Create min heap
    priority_queue<Node*, vector<Node*>, Compare> minHeap;

    for (auto& pair : frequency)
        minHeap.push(new Node(pair.first, pair.second));

    // Build Huffman Tree
    while (minHeap.size() > 1) {
        Node* left = minHeap.top();
        minHeap.pop();

        Node* right = minHeap.top();
        minHeap.pop();

        Node* parent = new Node('\0',
                                left->freq + right->freq);

        parent->left = left;
        parent->right = right;

        minHeap.push(parent);
    }

    Node* root = minHeap.top();

    // Generate Huffman Codes
    unordered_map<char, string> huffmanCode;
    generateCodes(root, "", huffmanCode);

    cout << "\n HUFFMAN CODES \n";

    for (auto& pair : huffmanCode) {
        if (pair.first == ' ')
            cout << "' ' : " << pair.second << endl;
        else
            cout << pair.first << " : " << pair.second << endl;
    }

    // Encoding
    string encoded;

    for (char ch : text)
        encoded += huffmanCode[ch];

    cout << "\n RESULT \n";
    cout << "Original Text : " << text << endl;
    cout << "Encoded Text  : " << encoded << endl;

    // Decoding
    string decoded = decode(root, encoded);

    cout << "Decoded Text  : " << decoded << endl;

    // Time Complexity
    int n = text.length();
    int k = frequency.size();

    cout << "\n TIME COMPLEXITY \n";
    cout << "Frequency Calculation : O(n)" << endl;
    cout << "Building Min Heap     : O(k log k)" << endl;
    cout << "Building Huffman Tree : O(k log k)" << endl;
    cout << "Generating Codes      : O(k)" << endl;
    cout << "Encoding              : O(n)" << endl;
    cout << "Decoding              : O(n)" << endl;
    cout << "-------------------------------------" << endl;
    cout << "Overall Time Complexity: O(n + k log k)" << endl;

    cout << "\nSpace Complexity: O(k)" << endl;

    return 0;
}
