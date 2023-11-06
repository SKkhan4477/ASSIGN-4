# ASSIGN-4
def merge_sort(arr):
    if len(arr) <= 1:
        return arr, 0
    mid = len(arr) // 2
    left, left_inversions = merge_sort(arr[:mid])
    right, right_inversions = merge_sort(arr[mid:])
    merged, split_inversions = merge(left, right)
    total_inversions = left_inversions + right_inversions + split_inversions
    return merged, total_inversions
def merge(left, right):
    merged = []
    inversions = 0
    i = j = 0
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            merged.append(left[i])
            i += 1
        else:
            merged.append(right[j])
            j += 1
            inversions += len(left) - i
    merged.extend(left[i:])
    merged.extend(right[j:])
    return merged, inversions
arr = [5, 2, 6, 1]
sorted_arr, inversions = merge_sort(arr)
print("Sorted Array:", sorted_arr)
print("Number of Inversions:", inversions)
q2:
class ListNode:
    def __init__(self, value=0, next=None):
        self.value = value
        self.next = next
def merge_sort_linked_list(head):
    if head is None or head.next is None:
        return head
    mid = find_middle(head)
    left_half = head
    right_half = mid.next
    mid.next = None
    left_half = merge_sort_linked_list(left_half)
    right_half = merge_sort_linked_list(right_half)
    return merge(left_half, right_half)

def find_middle(head):
    slow_ptr = head
    fast_ptr = head

    while fast_ptr.next is not None and fast_ptr.next.next is not None:
        slow_ptr = slow_ptr.next
        fast_ptr = fast_ptr.next.next

    return slow_ptr
def merge(left, right):
    dummy = ListNode()
    current = dummy
    while left is not None and right is not None:
        if left.value < right.value:
            current.next = left
            left = left.next
        else:
            current.next = right
            right = right.next

        current = current.next
    if left is not None:
        current.next = left
    else:
        current.next = right

    return dummy.next
def print_linked_list(head):
    current = head
    while current:
        print(current.value, end=" -> ")
        current = current.next
    print("None")
head = ListNode(5, ListNode(2, ListNode(6, ListNode(1))))
sorted_head = merge_sort_linked_list(head)
print("Sorted Linked List:")
print_linked_list(sorted_head)
q3:
def merge_sort_descending(arr):
    if len(arr) <= 1:
        return arr

    mid = len(arr) // 2
    left = arr[:mid]
    right = arr[mid:]

    left = merge_sort_descending(left)
    right = merge_sort_descending(right)

    return merge_descending(left, right)

def merge_descending(left, right):
    merged = []
    i = j = 0

    while i < len(left) and j < len(right):
        if left[i] >= right[j]:
            merged.append(left[i])
            i += 1
        else:
            merged.append(right[j])
            j += 1
    merged.extend(left[i:])
    merged.extend(right[j:])
    return merged
arr = [5, 2, 6, 1, 9, 3]
sorted_arr_descending = merge_sort_descending(arr)
print("Sorted Array in Descending Order:", sorted_arr_descending)
q4:
def multiway_merge_sort(arr):
    if len(arr) <= 1:
        return arr
    mid = len(arr) // 2
    left = arr[:mid]
    right = arr[mid:]
    left = multiway_merge_sort(left)
    right = multiway_merge_sort(right)
    return multiway_merge(left, right)
def multiway_merge(left, right):
    merged = []
    i = j = 0
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            merged.append(left[i])
            i += 1
        else:
            merged.append(right[j])
            j += 1
    merged.extend(left[i:])
    merged.extend(right[j:])
    return merged
arr = [5, 2, 6, 1, 9, 3, 4, 7]
sorted_arr = multiway_merge_sort(arr)
print("Sorted Array:", sorted_arr)


