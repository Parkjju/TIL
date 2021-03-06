# 트리 자료구조

### 트리란?

- 지금까지 해왔던 자료구조는 **링크를 따라 순차적으로 움직이는 sequential structure**
- 앞으로 배우게 되는 자료구조는 **부모-자식노드 관계에 따라 움직이게 됨. 상-하**

### 이진트리 용어들

1. 루트 노드 (root) - 가장 상위 노드
2. 링크(link), 에지(edge) - 각 노드를 서로 이어주는 선
3. 리프 노드 (leaf) - 각 링크의 가장 하위 노드
4. 레벨 (level) - 부모 노드와 자식 노드 사이의 간격 하나가 1레벨. (루트 노드는 레벨 0 부터 시작)
5. 트리의 높이 - 루트 노드로부터 가장 하위 리프 노드까지 필요한 링크의 수 (루트 노드와 가장 하위 리프 노드의 레벨 차이)
6. 경로(path) - 어떤 노드v ~ w까지 거쳐가는 노드들 (루트 3 -> 2 -> 7 -> 8 -> 12)
7. 경로 길이(path length) - 경로의 에지 개수
8. 부모 노드 (parent node) - 특정 노드의 바로 상위 노드
9. 자식 노드 (child node) - 특정 노드의 바로 하위 노드
10. 형제 노드 - 부모 노드가 동일한 노드

### 표현법

<img src="../Data_structure/images/tree.jpg" width="40%" height="40%"/>

- 리스트 - A = [ a,b,c,None,d,e,f,None,None,h,...... ]

  1. 루트 노드로부터 좌->우 방향으로 순회하면서 리스트에 값을 저장.
  2. 레벨이 증가할 때 해당 레벨만큼 필요한 자식 노드의 개수를 index 계산하여 무슨 레벨인지 파악
     - ex) 레벨이 2인 노드에 접근 -> 리스트의 인덱스 범위가 (2^2-1 ~ 2^3-1 까지)
  3. 노드에 값이 저장되어 있지 않으면 None 저장

- 리스트2 -> **재귀적 표현** A=[ a, [ a의 부트리 ], [ a의 오른쪽 부트리 ] ....]

  - [a, [b, [], [d, [ ], [ ] ], [ c, [e, [ ], [ ] ]].......]

- 노드 class를 정의
  - key
  - 자식 노드를 가리킬 link (left, right)
  - 부모 노드를 가리킬 parents
  - value 등등ㅇ.. 기타의 것들

### 이진 트리 (Binary Tree)

- 표현법

  1. 이진트리 -> 배열, 리스트 (heap)
  2. 노드와 링크를 직접적으로 표현 (노드 클래스를 구성) - Node, Binary Tree class

- 노드 클래스의 선언

```python
class Node:
    def __init__(self,key):
        self.key = key
        self.parent = self.left = self.right = None

    def __str__(self):
        return str(self.key)

def main():
    a = Node(6)
    b = Node(9)
    c = Node(1)
    d = Node(5)

    a.left=b
    a.right=c
    b.parent=a
    c.parent=a
    b.right=d
    d.parent=b
```

**순회 (Traverse)**

1. preorder
2. inorder
3. postorder

- 이진트리 순회 (traversal) : 이진트리 노드의 key값을 빠짐없이 출력하는 방법 -> **재귀적으로 구현!**
- M노드 : 자기자신, L : M의 left subtree, R : M의 Right subtree

1. preorder : M -> L -> R 순서
2. inorder : L -> M -> R 순서
3. postorder : L -> R -> M 순서

```python
class Node:
    def __init__(self,key):
        self.key = key
        self.parent = self.left = self.right = None

    def __str__(self):
        return str(self.key)

    def preorder(self): # self -> 현재 방문중인 노드
        if self!=None:
            print(self.key)
            if self.left:
                self.left.preorder()
            if self.right:
                self.right.preorder()

    def inorder(self):
        if self!=None:
            if self.left:
                self.left.inorder()
            print(self.key)
            if self.right:
                self.right.inorder()

    def postorder(self):
        if self!=None:
            if self.left:
                self.left.postorder()
            if self.right:
                self.right.postorder()
            print(self.key)
```

- 상황가정) 이진트리의 모양을 모르는 상태.
  1. preorder : F B A D C E G I H
  2. inorder : A B C D E F G H I
- 이로부터 원래의 이진트리의 모양을 복원하는 작업 -> **reconstruct** - Inorder를 포함하여, preorder와 postorder 중 순서 개념을 알고 있는 상태로 이진트리 배열이 주어지면 reconstruct가 가능하다.

* 위의 상황가정의 경우 reconstruct가 가능!!

### 이진 탐색 트리(Binary search Tree)

- 탐색 기능에 효율적으로 이용되는 자료구조
- 각 노드의 왼쪽 subtree의 key값은 노드의 key값보다 작거나 같아야함.
- 각 노드의 오른쪽 subtree의 key값은 노드의 key값보다 커야함.
- `A = [15,4,20,None,2,17,32,None,None,None,19,None,None]`
- **루트노드 뿐만 아니라 모든 노드에 있어서 해당 규칙이 적용되어야 함.**

- 15(루트 노드) > 왼쪽 subtree(4), 15(루트 노드) < 오른쪽 subtree(20)

- search(19) -> 루트부터(15) 시작 - 15보다 크므로 오른쪽 subtree -> 20보다 작음 - 20의 왼쪽 subtree -> .....

- level by level로 내려감 -> 한 레벨마다 작을 지 클 지 판단됨 -> O(h), h==height.
- 트리 자료구조 -> height를 최대한 작게 유지 !!!

```python
class BST:
    def __init__(self):
        self.root=None
        self.size=0

    def __len__(self):
        return self.size

    def __iter__(self):
        return self.root.__iter__() # Node class의 iter 스페셜메소드 호출, BST class 말고!!!
    # iter메소드는 제너레이터로 정의하기

T = BST()
T.insert(15)
T.insert(4)
#       15
#   4       None, 4가 15의 왼쪽subtree로 들어가야함. 그렇게 되도록 insert메소드를 구현!!
```

- find_location 메소드

```python
class BST:
    # .....
    def find_loc(self,key): # key 값 노드가 있다면 해당 노드를 return, 없다면 삽입될 위치의 부모노드를 리턴
        if self.size==0:
            return None
        p = None # 한방향 연결리스트 tail찾기와 비슷한 방식
        v = self.root
        while v!=None:
            if v.key==key:
                return v
            elif v.key < key:
                p = v
                v = v.right
            else:
                p = v
                v = v.left
        # while을 빠져나옴 ->그 동안 따라왔던 부모노드 p를 리턴.
        return p

    def search(self,key):
        v = self.find_loc(key)
        if v == None:
            return None
        else:
            return v

    def insert(self,key):
        p = self.find_loc(key) # : O(h) -> 상수시간
        # p와 v의 링크를 달아줌
        if p==None or p.key!=key:
            v = Node(key)
            if p == None:
                self.root = v # p는 부모노드인데, None이므로 루트노드
            else: # p가 루트노드가 아니면서, p의 key값이 insert할 key와 값이 다르다. - 정상적인 상황
            # insert할 key의 왼쪽에 들어갈 지, 오른쪽에 들어갈 지 모르는 상황
                v.parent = p
                if p.key > key:
                    p.left = v
                else:
                    p.right = v
            self.size+=1
            return v
        else:
            print("key is already in tree") # tree에 존재하는 key값을 다시 insert하려는 시도를 했다고 알려주는 부분
            return p
```

- 삭제연산(delete) : deleteByMerging, deleteByCopying

  - deleteByMerging(self,x) -> 노드 x를 삭제.
  - deleteByCopying

- deleteByMerging(self,x)
  - 왼쪽 subtree를 L, 오른쪽 subtree를 R
  - 삭제한 x 자리에 L이 오도록 함
  - 가장 큰 key값을 가진 노드를 m이라고 할때 해당 노드에 R을 연결한다.
  - L의 루트노드와 삭제한 x노드의 부모 노드와 link update
- 특수한 경우
  1. a==None -> b가 x를 대체
  2. x == root -> x가 트리의 루트노드가 아니면 L이 그냥 x를 대체하면 됨

```python
# pseudo code
def deleteByMerging(self,x):
    a = x.left
    b = x.right
    c = x자리를 대체할 노드
    m = L에서 key가 가장 큰 노드 # L에서 key값이 가장 큰 노드
    pt = x.parent
    if a!=None:
        c = a
        m = a
        while m.right:
            m = m.right
        if b!=None:
            b.parent = m
            m.right = b
        else: # a==None
            c = b
        # x를 대체한 뒤에 x의 부모와 대체한 노드의 링크를 업데이트

        if pt!=None:
            if c:
                c.parent = pt
            if pt.key < c.key:
                pt.right = c
            else:
                pt.left = c
        else: # x.parent==None -> 루트노드
            self.root = c
            if c: # c가 none이 아니어야함
                c.parent=None

        self.size -= 1
```

- deleteByCopying

  - L이 존재
    1. L에서 가장 큰 값을 갖는 노드 y를 찾는다
    2. y의 key값을 x의 key값으로 카피
    3. y의 left subtree가 존재하면, y의 위치로 올린다.
  - L이 존재하지 않고, R이 존재하는 경우
    1. R에서 가장 작은 값을 갖는 노드 y를 찾는다
    2. y의 key값을 x의 key값으로 카피한다.
    3. y의 right subtree가 존재하면, y의 위치로 올린다.
  - 삭제할 노드가 root인 경우

* 삭제 및 연산수행을 진행할 때에 각 노드마다 height정보를 관리한다면 update해야하는 경우 생각하여 진행 (추가 및 삭제된 노드 대상과 관련된 노드만 확인하면됨)

- **deleteByMerging, deleteByCopying 수행시간**

  - 두 함수 모두 L, 즉 삭제할 x노드의 left subtree의 maximum key를 찾는 데에 가장 많은 시간을 사용한다.
  - 최악의 경우 O(h)시간

- 따라서 이진탐색트리에 있어서 insert, search, delete-merging and copying에 있어서 모두 최악의 경우 O(h)시간이 걸린다.
  - 이진 탐색트리의 h에 있어서 수행시간의 차이가 분명 존재할 것이다.
  - h를 최소화 하도록 강제적으로 하는 이진탐색트리를 **balanced-binary tree**라고 함.

#### 균형이진탐색트리 balanced-binary tree

- 균형이진탐색트리 - 트리의 높이가 로그의 밑이 2인 logn만큼 비례되어 형성되는 트리

- 트리의 높이를 줄이는 연산 - **Rotation - 회전** \* Right rotation - left subtree의 높이가 더 깊을때 진행.
  <img src="images/right-rotation.jpg" height="60%" width="60%"/>

- rotateRight정의

```python
def rotateRight(self,z):
    if not z:
        return
    x = z.left
    if x==None:
        return
    b = x.right
    x.parent = z.parent
    if z.parent:
        if z.parent.left == z:
            z.parent.left = x
        else:
            z.parent.right = x
    x.right = z
    z.parent = x
    z.left = b
    if b:
        b.parent = z
    if self.root == z:
        self.root = x
```

#### AVL 트리 (Adelson-Velsky, Landis)

- AVL트리란? 모든 노드에 대해서 각 노드의 left subtree와 right subtree의 높이 차가 1이하인 BST
- AVL 트리는 n개의 노드에 대해서 항상 높이가 logn 시간으로 만들어지는가?

- proof
  1. h = 0 AVL -> 루트노드가 AVL트리가됨
  2. h = 1
     - root - left, root - right, root - right & left
     - 세 트리 모두 노드 수가 2,3개 이므로 logn 시간에 높이 형성
  3. h = 2
     - AVL정의에 입각하여 높이를 형성하여 확인해보기..
  4. 높이의 일반화 -> 각 높이에 따라 노드 수가 최소인 경우를 생각
     - 루트노드로부터 left subtree와 right subtree의 높이 차가 1인 경우
     - N_h = 높이가 h인 AVL트리 중에서 최소 노드의 개수
     - N_0 = 1, N_1 = 2, N_2 = 4, N_3 = 7
     - N_h -> left subtree의 갯수 N_h-1 & right subtree의 갯수 N_h-2 => N_h = N_h-1 + N_h-2 + 1
     - N_h >= 2\*N_h-2 + 1 >= 2\*N_h-2
     - N_h >= 2\*N_h-2 >= 2\*(2\*N_h-4)
     - ......
     - 2^(h/2)\*N_0 = 2^(h/2)
     - N_h >= 2^(h/2)
- 결론 - 높이 h이고 노드 갯수가 n인 AVL트리를 가정
  - h <= c\*log2(n)을 증명?
  - n >= N_h >= 2^(h/2)
  - h/2 <= log2(n)
  - h <= 2\*log2(n) => h = O(log2(n))

```python
class Node:
    # BST와 동일 + key, left, right, parent, height추가해야됨
class BST:
    #insert, deleteByMerging, search, deleteByCopying활용하는 BST 잘 이용하면됨.
    #insert와 deleteBymerging&Copy는 height 변하는 노드에 대해 Update하도록 추가 구현 필요
    # + insert및 delete시 AVL정의를 유지하지 못하는 경우에 대해 처리는 나중에
class AVL(BST):
    # BST상속 - git정리내용 참고
    # init함수 없어도 됨 - BST클래스에서 구현해놓았기 때문
    def insert(self, key):
        v = super.(AVL,self).insert(key) # AVL클래스의 self객체에 대하여 부모 클래스의 메소드인 insert메소드를 호출해라~
        # v의 삽입전, v의 삽입으로 인해 AVL정의가 무너지는 경우를 생각하자 - rebalance
        # 1. find x,y,z -> 처음으로 AVL조건이 깨진 노드
        w = rebalance(x,y,z)
        if w.parent == None:
            self.root = w

```

- rebalance 이미지 - 신찬수교수님 유튜브 AVL강의
  <img src="images/rotate.png" width="60%" height="60%"/>

* z노드 - insert된 노드로부터 거슬로 올라가다가 가장 처음으로 AVL조건에 위배되는 노드 . x와 y는 leaf노드의 조상이면서 z의 자식노드(z-y-x)

- insert이후 rebalance 1회 또는 2회를 진행하면 AVL을 만족하게됨.
- AVL에서 insert 수행시간 -> super의 insert -> O(h) = O(logn)

  - find -> O(logn)
  - rebalance -> O(1)
  - self.root=w -> O(1)

- delete연산
  <img src="images/delete.png" width="60%" height="60%"/>

- insert에서는 insert된 leaf node로부터 거슬러 올라가 rebalance를 진행했다면, delete는 삭제 이후 반대쪽 subtree(더 무거운 부트리)로부터 노드를 나눠받아 rebalance를 진행한다.
- delete 이후 rebalance를 진행하였는데, rebalance를 마친 후의 tree의 부모 노드 입장에서 AVL이 만족되지 않는 상황이 발생 (그림 3)
  - AVL 만족이 루트노드까지 이루어지는지 확인해야함.
  - insert에서 1회 및 2회에서 rebalance가 마무리지어진다면 O(1)
  - delete에서는 최악의 경우 높이만큼 rotation을 진행 O(logn)

```python
#pseudo code
def delete(self,u):
    v = super(AVL,self).deleteByCopying(u) # u라는 노드를 지우면, u노드 삭제 이후로 AVL조건이 꺠질 수 있는 가능성이 가장 큰 노드를 반환하도록 설계
    while v!=None: #루프까지 AVL만족하도록 check
        if v is not balanced:
            z = v
            if z.left.height >= z.right.height:
                y = z.left
            else:
                y = z.right

            if y.left.height >= y.right.height:
                x = y.left
            else:
                x = y.right
            # 여기까지 x-y-z관계가 설정됨
            v = rebalance(x,y,z) # x-y-z가 일직선 연결 -> 1회 rotation, 중간에 구부러짐 -> 2회 로테이션, 그림에서는 그림 3의 y가 리턴됨
            w = v
            v = v.parent # 그림 3에서 w는 v로, y자리에 w가 있어야함. (수정.) w가 v를 한 자리 뒤에서 따라가는 형태
```

- AVL정리
  - 높이 <= 2logn => O(logn)
  - insert - 노드 삽입 O(logn) + rebalance(1회 및 2회) O(1) => O(logn)
  - delete - 노드 제거 O(logn) + rebalance(최악의 경우 O(logn)) => O(logn)

#### Red-Black tree

- 가장 유명하고 많이 사용되는 균형이진탐색트리.

<img src="images/red-black.png" width="60%" height="60%"/>

- NIL노드 == NULL노드, NULL 안쪽 노드는 내부노드로 불림.

- 특징

  1. 노드들은 red or black의 색만 가진다.
  2. root노드는 black이다.
  3. leaf노드 (NULL노드)는 black이다
  4. red노드는 두개의 자식노드를 가진다 (NULL 노드도 표기하기 때문) + red노드는 자식을 black만 가질 수 있다.
  5. 각 노드에서 leaf노드로 가는 경로들 사이에 **거치는 black노드의 개수가 동일해야한다** - height가 평균 logn시간에 만들어진다는 것을 증명할 때 이용

- 정의

  - h(v) = v의 높이 (height)
  - bh(v) = v에서 leaf까지 가는 동안 만나는 black노드의 갯수 **(v는 제외해야함.)**

- 증명
  1. v의 서브트리의 내부노드 갯수 >= 2^(bh(v)) - 1
     - h(v)에 대한 귀납법을 통해 증명 (induction)
     - Base case => h(v)=0 -> v의 내부노드 갯수 >= 2^0 - 1 => 성립
     - Hypothesis phase => h(v) <= k에 대하여 **|v의 서브트리| >= 2^bh(v) - 1**임을 가정
     - 귀납법 시작. -> h(v) = k + 1일때 **|v의 서브트리| >= 2^bh(v) - 1**이 성립함을 증명
     - bh(w) & bh(z) = {bh(v) or bh(v-1)}
       - pf) bh(v)로부터 w또는 z를 거쳐 만나는 black node의 수들을 생각하면, w또는 z가 black노드인 경우를 제외하면 만나는 black 노드의 수가 모두 동일하다.
     - 따라서, |v의 subtree내부노드 수| >= 2^bh(w) - 1 + 2^bh(z) - 1 + 1 = 2^bh(v) - 1
     - -> |v의 subtree의 내부노드 수| >= 2^bh(v) - 1임을 결국 증명!!!!
  2. black 노드 수(root로부터 leaf까지 가는동안 만나는 black노드 수 - bh(root)) >= h/2 (red보다 black노드가 더 많을 수 없음. ) - red자식노드는 무조건 black 노드여야 하기 때문
     - r의 subtree의 내부노드 개수 == 전체 red-black tree의 전체 노드 수 >= 2^bh(root) - 1 >= 2^(h/2) - 1
     - n >= 2^(h/2) - 1
     - h/2 <= log2(n+1) -> h <= 2log2(n+1)
     - **결론** => h = O(log2(n)) => red-black노드는 BST이다 !!

<img src="images/black-height.jpg" width="60%" height="60%"/>

#### Red-Black트리의 삽입연산

- BST의 insert연산을 호출 - 새로운 노드를 삽입(x)
- x.color = red
- 4가지 경우로 나누어 조정.

<img src="images/rbinsert.png" height="60%" width="60%" />

- 경우

  1. empty red-black트리에 x를 삽입
     - red로 삽입했던 x를 black으로 바꾸기 - x.color = black
  2. x.parent.color == black
     - do nothing
  3. x.parent.color == red
     1. x.uncle.color == red인 경우 (uncle => parent노드의 형제 노드)
        - grandparent노드는 black이어야 함.(parent노드가 red인 상황이기때문)
        - grandparent.color = red로 변경한 뒤 parent노드를 red에서 black, uncle노드를 red에서 black으로 바꾼다
        - 색이 red으로 변한 grandparent입장에서, leaf까지 내려가는 동안 만나는 black노드의 수는 변하지 않는다 (원래 grandparent 자신에게 있던 black을 parent와 uncle에게 주었기 때문)
        - 색이 black으로 변한 parent 입장에서, leaf까지 내려가는 동안 만나는 black노드의 수는 +1로 변한다.
        - uncle도 parent와 마찬가지
        - parent와 uncle입장에서 black노드의 개수가 증가했다고 해도, 전체적으로 보면 black노드 수가 동일하기 때문에 괜찮다
     2. x.uncle.color == black인 경우
        1. x - parent - grandparent : linear인 경우
           - grandparent에서 right rotation을 진행
           - grandparent의 색을 red로 변경 -> 색 조건 + 거쳐가는 black노드 수 동일
        2. x- parent - grandparent : triangle인 경우
           - parent에서 left rotation
           - grandparent에서 right rotation
           - grandparent를 red로 변경 -> 색 조건 + 거쳐가는 black 노드 수 동일

- 수행시간

  - 회전은 최대 2번 : O(1)
  - 색깔을 조정 : O(1)
  - 최종 O(logn) - BST class에서 가져온 insert 수행시간이 O(logn)이기 때문 !

- delete의 수행시간도 O(logn)에 가능하다.

  - 회전 수는 상수이지만, deleteByMerging or copy연산 자체가 logn시간.

- AVL vs Red-Black rotation수

  - search - -
  - insert 2 2
  - delete O(logn) 3

- [Red - Black트리 위키](https://ko.wikipedia.org/wiki/%EB%A0%88%EB%93%9C-%EB%B8%94%EB%9E%99_%ED%8A%B8%EB%A6%AC)

#### 2,3,4트리 - Red Black트리와의 관계가 밀접한 트리

- 2,3,4트리 조건
  1. 자식노드의 개수가 2,3,4개중 하나
  2. 모든 leaf node가 같은 level에 존재
- 2-노드, 3-노드, 4-노드

<img src="images/two.png" height="60%" width="60%" />

- 노드 search방법

  - search(53) -> a <= b <= c인 자식 노드와 비교하면 됨. =>4갈래

- 높이

  - root를 제외한 모든 자식노드가 4개인 경우 - log4(n)
  - root를 제외한 모든 자식노드가 2개인 경우 - log2(n)
  - h = O(log2(n))인 균형탐색트리 (**이진트리 아님!!**)

- insert(key)
  - search해나가다가, 삽입할 공간이 있으면 삽입
  - **4-노드를 만나면 split하면서 리프노드까지 내려감** - insert될 key가 search하려고 노드에 들어가봤더니 4-노드가 된 경우를 4-노드와 만났다고 표현
  - \[a,b,c\] 노드가 있을때, b를 부모로 보내고 a와 c로 쪼개는 연산이 split (one split -> O(1))
  - 모든 level에서 split이 발생 -> h가 O(logn)이므로 insert연산도 O(logn)
  - 루트노드가 4-노드가 되면 height가 증가하게됨.

<img src="images/split.png" width="60%" height="60%" />

- delete(key)

  - [2-3-4 tree wiki 中 Deletion 발췌](https://en.wikipedia.org/wiki/2%E2%80%933%E2%80%934_tree)
  - 삭제할 key값이 트리 내부에는 존재하는데, leaf node에 있을수도 없을수도 있다.
  - 삭제할 key값이 leaf node에 없는 경우 successor연산을 통해 삭제 대상인 key값보다 큰 **바로 다음 수를 찾는다**
  - successor는 항상 leaf node에 있으며, successor가 없으면 key보다 작은 **바로 이전 수를 찾는다**
  - successor를 찾았으면 삭제 대상인 key값과 swap후 key를 삭제
  - 어쨌든 key값을 가진 노드는 swap하던 원래 leaf node에 있던 leaf node에 있을 것이기 때문에 leaf node에 있다고 가정하자.

- delete의 경우, 사진에서 70key를 가진 노드를 지운다면 70의 부모인 80노드가 자식노드를 하나밖에 갖지 못한다. => **2-3-4 tree 정의에 위배**
  - 삭제할 노드를 찾아 search하는 과정에서, 루프->리프까지 가는 동안 2-노드를 만나면 3-노드로 바꾼다 (그림 보고 흐름 이해해보기)
  - 왼쪽 그림의 경우 30노드 기준 형제 노드로부터 자신을 3-노드로 바꿀 수 있게끔 노드를 꿔올 수 있는지 본다. -> 30노드 3-노드로 바꿔줌
  - 오른쪽 그림의 경우 30노드 기준 형제 노드를 보니, 형제 노드들도 모두 2-노드여서 꿔올 수 없는 상황 => 부모의 key와 적당히 병합하여 3 or 4-노드로 만들어준다 -> **fusion**
  - root노드 입장에서 자식노드를 3 or 4노드를 만드는 연산은 없으며, root의 자식 노드 모두 2-노드라면 root와 자식노드들을 fusion한다! => height가 줄어듦

<img src="images/deletetwo.png" height="60%" width="60%" />

- delete수행시간
  - fusion이 레벨마다 일어나면 -> O(logn)시간

#### 2-3-4트리와 Red-black트리의 관계성

- [Converting a 2-3-4 tree into a red black tree](https://stackoverflow.com/questions/35955246/converting-a-2-3-4-tree-into-a-red-black-tree)
- 2-3-4에서 Red-black으로

  1. 2-node -> black으로
  2. 3-node -> 2 level에 걸쳐서 쪼개기. 쪼갠 뒤 색 부여 (첫번째 레벨에 black, 두번째 레벨에 red)
  3. 4-node도 2 level에 걸쳐 쪼개기 (첫번째 레벨에 black, 두번째 레벨에 red)

  - **만약, 3-node나 4-node가 red-black트리로 변환되면서 만들어내는 black노드의 수에 차이가 있다면, ex) 3-node는 1개 만들어내는데 4-node는 2개를 만들어낸다면, root로부터 쭉 내려올때 left subtree에 3-노드를 포함하고, right subtree에 4-노드를 포함하는 경우 red-black트리의 대전제를 깨게 됨**
  - 3-node도, 4-node도 레드 블랙트리로 변환하면 레벨당 하나씩 블랙노드를 매핑하기때문에 문제가 발생하지 않음!!!

- 2-3-4 tree의 높이를 h, 이에 대응되는 red-black tree의 높이를 h'이라고 하자
  - log4(n) <= h <= log2(n)임은 위에서 확인했었음.
  - 높이가 h인 2-3-4트리를 red-black으로 대응시킬때, 최악의경우 2-3-4트리 모두가 3-node로 이루어져있는 것 -> 두 레벨로 쪼개져서 대응됨.
  - 결론적으로, h' <= 2\*h가 되고, h' <= 2\*log3(n) = (2/log2(3))\*log2(n) = 1.261\*log2(n)
