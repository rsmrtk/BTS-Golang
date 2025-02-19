package main

import "fmt"

// Node represents a single node in the binary search tree.
// Нода представляє один вузол у бінарному дереві пошуку.
type Node struct {
value int   // Значення вузла
left  *Node // Вказівник на лівого нащадка
right *Node // Вказівник на правого нащадка
}

// BinaryTree is a structure that represents the binary search tree.
// BinaryTree - структура, що представляє бінарне дерево пошуку.
type BinaryTree struct {
root *Node // Кореневий вузол дерева
}

// Insert adds a new value to the binary search tree.
// Insert додає нове значення у бінарне дерево пошуку.
func (t *BinaryTree) Insert(value int) {
if t.root == nil {
t.root = &Node{value: value} // Якщо кореня немає, створюємо його
} else {
insertNode(t.root, value) // Вставка рекурсивним способом
}
}

// insertNode recursively inserts a new node into the binary search tree.
// insertNode рекурсивно додає новий вузол у бінарне дерево пошуку.
func insertNode(node *Node, value int) {
if value < node.value {
if node.left == nil {
node.left = &Node{value: value} // Додаємо вліво, якщо лівий вузол порожній
} else {
insertNode(node.left, value) // Рекурсивний виклик для лівого піддерева
}
} else {
if node.right == nil {
node.right = &Node{value: value} // Додаємо вправо, якщо правий вузол порожній
} else {
insertNode(node.right, value) // Рекурсивний виклик для правого піддерева
}
}
}

// inorder performs an in-order traversal (left, root, right).
// inorder виконує обхід у порядку (ліво, корінь, право).
func inorder(node *Node) {
if node != nil {
inorder(node.left)
fmt.Print(node.value, " ") // Друкуємо значення вузла
inorder(node.right)
}
}

// preorder performs a pre-order traversal (root, left, right).
// preorder виконує обхід у порядку (корінь, ліво, право).
func preorder(node *Node) {
if node != nil {
fmt.Print(node.value, " ") // Друкуємо значення вузла
preorder(node.left)
preorder(node.right)
}
}

// postorder performs a post-order traversal (left, right, root).
// postorder виконує обхід у порядку (ліво, право, корінь).
func postorder(node *Node) {
if node != nil {
postorder(node.left)
postorder(node.right)
fmt.Print(node.value, " ") // Друкуємо значення вузла
}
}

func main() {
tree := &BinaryTree{} // Створюємо нове бінарне дерево пошуку

	// Вставляємо значення, щоб отримати збалансоване дерево
	tree.Insert(4)
	tree.Insert(2)
	tree.Insert(6)
	tree.Insert(1)
	tree.Insert(3)
	tree.Insert(5)
	tree.Insert(7)

	fmt.Println("In-order traversal")
	inorder(tree.root)
	fmt.Println()

	fmt.Println("Pre-order traversal")
	preorder(tree.root)
	fmt.Println()

	fmt.Println("Post-order traversal")
	postorder(tree.root)
	fmt.Println()
} 
