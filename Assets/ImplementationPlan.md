# Implementation Plan - Implement Array from scratch (Triển khai mảng động từ đầu)

This plan outlines the steps to implement a custom dynamic array (similar to `List<T>`) from scratch and create a UI to interact with it, including demonstrating an index-out-of-bounds "crash".

Bản kế hoạch này phác thảo các bước để triển khai một mảng động tùy chỉnh (tương tự `List<T>`) từ đầu và tạo giao diện người dùng để tương tác, bao gồm cả việc minh họa lỗi "crash" do truy cập ngoài phạm vi.

## Proposed Changes

### 1. Data Structure Implementation (Triển khai Cấu trúc Dữ liệu)
- **File**: `Assets/Array.cs`
- **Class**: `MyDynamicArray<T>`
- **Logic**:
    - Internal fixed-size array (`T[]`).
    - `Count` to track actual items.
    - `Add(T item)`: Double capacity when full.
    - Indexer `[int index]` with explicit bounds checking.

### 2. UI Development (Phát triển Giao diện)
- **File**: `Assets/ArrayUI.cs` (New)
- **File**: `Assets/ArrayUI.uxml` (New)
- **File**: `Assets/ArrayUI.uss` (New)
- **Features**:
    - Add item input.
    - Scroll view to see array contents.
    - Visual indicators for Capacity vs Count.
    - "Crash Test" button to trigger `IndexOutOfRangeException`.

### 3. Documentation (Tài liệu hóa)
- **File**: `Assets/Docs/DSA_101.md`
- **Content**: Add a section on "Dynamic Array Implementation" with Vietnamese explanations of time complexity and resizing logic.

## User Rules Compliance
- **UI Toolkit First**: Using UXML and USS for the interface.
- **Explicit Typing**: All variables will be explicitly typed.
- **Vietnamese Explanations**: Included in this plan and documentation.
- **English Comments**: All code comments will be in English.

## Execution Steps

1. Create the `MyDynamicArray` class in `Array.cs`.
2. Create `ArrayUI.uxml` and `ArrayUI.uss` for the visual layout.
3. Create `ArrayUI.cs` to handle UI logic and interaction with `MyDynamicArray`.
4. Update `DSA_101.md` with the new knowledge.
- **Verification**: Test the Add and Crash functions in the Unity Editor.

## Usage / Cách sử dụng
To see the UI in action:
1. Create a new GameObject called **ArrayManager** in your scene.
2. Add `UIDocument`, `Array`, and `ArrayUI` components to it.
3. Drag `Assets/ArrayUI.uxml` into the **Visual Tree Asset** field of the `UIDocument`.
4. Press **Play** and interact with the UI.

Để xem giao diện hoạt động:
1. Tạo một GameObject mới tên là **ArrayManager** trong scene.
2. Thêm các component `UIDocument`, `Array`, và `ArrayUI` vào đó.
3. Kéo file `Assets/ArrayUI.uxml` vào ô **Visual Tree Asset** của `UIDocument`.
4. Nhấn **Play** và tương tác với giao diện.
