# HanoiTowers
## Giới Thiệu:
Sử dụng thư viện d3js để vẽ hình và tạo animation chuyển động cho các đĩa.  
Sử dụng Lập trình hướng đối tượng (JavaScript ES6) để giải quyết thuật toán của bài toán Tháp Hà Nội.  

## Logic  
#### Sử dụng thuật toán Đệ Quy để giải quyết bài toán:  
```javascript
var hanoi = function(disc,src,aux,dest){
  if(disc > 0){
    hanoi(disc -1,src,dest,aux);
    console.log('Move disc '+disc+' from '+src+' to '+dest);
    hanoi(disc -1,aux,src,dest);
  }
};
hanoi(3,'src','aux','dest');
```
#### Trong đó:    
* src,aux,dest là các Tháp tương ứng: Tháp gốc (src),Tháp trung gian(aux) và Tháp Đích.
* disk là tham số dạng Number tương ứng số đĩa truyền vào.
#### Cách giải  
* Chuyển n-1 đĩa từ cọc A sang B. Chỉ còn đĩa n trên cọc A.  
* Chuyển đĩa n từ cọc A sang cọc C.  
* Chuyển n-1 đĩa từ B sang C cho các đĩa có đường kính nhỏ hơn lần lượt nằm trên đĩa n.  
* Tiến hành bước 1 và 3, áp dụng lại thuật giải cho n-1.  
## Sử dụng Class trong JSES6 để lập trình OOP giải quyết bài toán Tháp Hà Nội
#### Chia Bài toán ra 3 Class: 
* Class Disk,class Tower và Class GameEngine để chạy chương trình.  
* Class Disk chứa các thuộc tính của Đĩa và phương thức draw để vẽ đĩa:
```javascript
class Disk {
	constructor(nameDisks, d) {   //tham số truyền vào
	
		//Định nghĩa thuộc tính tên Đĩa cho class Disk
		this.name = nameDisks 
		//Định nghĩa thuộc tính số thứ tự hay bán kính,các đĩa có bán kính lớn hơn thì ở dưới
		this.diameter = d    
		
	}
	drawDisk(...) {
		//phương thức vẽ
	}
}
```
* Class Tower chứa các thuộc tính của Tower và phương thức draw để vẽ tower:
```javascript
class Tower {
	constructor(nameTowers, arrDisk) { //tham số truyền vào
		//Định nghĩa thuộc tính Tên Tháp
		this.name = nameTowers 
		//Định nghĩa thuộc tính mảng chứa các Đĩa
		this.arrDisk = arrDisk 
	}
	drawTower(...) {
		//phương thức vẽ
	}
}
```
* Class GameEngine chứa logic xử lý bài toán:
```javascript
class GameEngine {
	constructor() {
		//đếm các bước thực hiện bài toán
		this.count = 0 
	}

	//Phương thức để giải quyết bài toán tháp hà nội
	move(n, a, b, c) {
		if (n > 0) {
			this.move(n - 1, a, c, b)
			console.log(`Move disk ${n} from ${a.name} to ${c.name}`);
			this.count++; //count the count
			this.move(n - 1, b, a, c)
		}
	}
	
	animateDisk(...) {
		//phương thức animation
	}
}
```
* Khai báo các Instances (hình mẫu) của Đối tượng Disk,Tower,GameEngine và chạy chương trình:
```javascript
diskArr = [
	new Disk('disk1',1),
	new Disk('disk2',2),
	new Disk('disk3',3),
	new Disk('disk4',4)
]

towerArr = [
	new Tower('tower1'),
	new Tower('tower2'),
	new Tower('tower3'),
]

let game = new GameEngine()
console.log(`Truyền vào ${diskArr.length} Đĩa`)
game.move(diskArr.length, towerArr[0], towerArr[1], towerArr[2],)
console.log(`Tổng cộng ${game.count} bước`)
```
* Cuối cùng là Kết Quả in ra Console:
```
Truyền vào 4 Đĩa

Move disk 1 from tower1 to tower2  js.js:51:4
Move disk 2 from tower1 to tower3  js.js:51:4
Move disk 1 from tower2 to tower3  js.js:51:4
Move disk 3 from tower1 to tower2  js.js:51:4
Move disk 1 from tower3 to tower1  js.js:51:4
Move disk 2 from tower3 to tower2  js.js:51:4
Move disk 1 from tower1 to tower2  js.js:51:4
Move disk 4 from tower1 to tower3  js.js:51:4
Move disk 1 from tower2 to tower3  js.js:51:4
Move disk 2 from tower2 to tower1  js.js:51:4
Move disk 1 from tower3 to tower1  js.js:51:4
Move disk 3 from tower2 to tower3  js.js:51:4
Move disk 1 from tower1 to tower2  js.js:51:4
Move disk 2 from tower1 to tower3  js.js:51:4
Move disk 1 from tower2 to tower3  js.js:51:4

Tổng cộng 15 bước
```
## Animation

