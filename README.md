# Word-Ladder

class Solution {
public:
    int ladderLength(string beginWord, string endWord, vector<string>& wordList) {
        unordered_set<string> dic(wordList.begin(), wordList.end());
        if (!dic.count(endWord)) return 0;

        queue<string> q;
        q.push(beginWord);
        int count = 1;

        while (!q.empty()) {
            int size = q.size();

            while (size--) {
                string word = q.front();
                q.pop();

                if (word == endWord) {
                    return count;
                }

                for (int i = 0; i < word.size(); i++) {
                    char x = word[i];

                    for (char c = 'a'; c <= 'z'; c++) {
                        if (c == x) continue;

                        word[i] = c;
                        if (dic.count(word)) {
                            q.push(word);
                            dic.erase(word);
                        }
                    }
                    word[i] = x;
                }
            }
            count++;
        }
        return 0;
    }
};
