**⏩ 문제**

1) 다음 **트리**를 Preorder 운행법으로 운행한 결과는?

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7460b3a0-92a4-4ab3-8b0a-e3e880f1c1ae/Untitled.png)

정답: ＋ * * / A B C D E

2) 다음 **트리**를 Preorder 운행법으로 운행할 경우 가장 먼저 탐색되는 것은?

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/357f8df1-264d-4bc2-8c69-587fb3d50290/Untitled.png)

정답: A

3) 다음 **트리**에 대한 INORDER 운행 결과는?

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e91fe724-1d84-42c3-b95b-1a6cc2142df1/Untitled.png)

정답: D B A E C F

4-1) 다음 코드는 어떤 순회를 구현한 것인지 서술하시오.

4-2) left-root-right 방식으로 운행하는 순회를 구현하기 위해서는 다음 코드를 어떻게 바꿔야 하는지 서술하시오.

```python
    def function (self, node):
        if node != None:
            if node.left:
                self.function(node.left)
            if node.right:
                self.function(node.right)
            
            print(node.data, end = ' ')
```

4-1 정답: postorder (후위순회)

4-2 정답: 

```python
    def inorder(self, node):
        if node != None:
            if node.left:
                self.inorder(node.left)
            
            print(node.data, end = ' ')

            if node.right:
                self.inorder(node.right)
```
