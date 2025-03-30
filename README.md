
#include <iostream>
#include <vector>
#include <algorithm>
#include <ctime>

int sequentialSearch(const std::vector<int>& data, int target) {
    for (int i = 0; i < data.size(); i++) {
        if (data[i] == target) {
            return i;
        }
    }
    return -1;
}

int binarySearch(const std::vector<int>& data, int target) {
    int left = 0, right = data.size() - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (data[mid] == target) {
            return mid;
        }

        if (data[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    return -1;
}

int main() {
    int n, target;
    
    std::cout << "Enter the number of data items: ";
    std::cin >> n;

    std::vector<int> data(n);
    
    std::cout << "Enter the data items: ";
    for (int i = 0; i < n; i++) {
        std::cin >> data[i];
    }

    std::cout << "Enter the target element to search for: ";
    std::cin >> target;

    clock_t start = clock();
    int seqResult = sequentialSearch(data, target);
    clock_t end = clock();
    double seqTime = double(end - start) / CLOCKS_PER_SEC;

    std::sort(data.begin(), data.end());

    start = clock();
    int binResult = binarySearch(data, target);
    end = clock();
    double binTime = double(end - start) / CLOCKS_PER_SEC;

    std::cout << "Sequential Search: ";
    if (seqResult != -1) {
        std::cout << "Found at index " << seqResult << std::endl;
    } else {
        std::cout << "Not found" << std::endl;
    }
    std::cout << "Time taken for Sequential Search: " << seqTime << " seconds" << std::endl;

    std::cout << "Binary Search: ";
    if (binResult != -1) {
        std::cout << "Found at index " << binResult << std::endl;
    } else {
        std::cout << "Not found" << std::endl;
    }
    std::cout << "Time taken for Binary Search: " << binTime << " seconds" << std::endl;

    if (seqTime < binTime) {
        std::cout << "Sequential Search is more efficient." << std::endl;
    } else {
        std::cout << "Binary Search is more efficient." << std::endl;
    }

    return 0;
}

 
