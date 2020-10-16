# MultiAgent
 INT3401_8

 Mô tả cách cài đặt cho các câu hỏi trong bài:
 - Question 1: Đầu tiên lấy ra list vị trí của thức ăn ở trạng thái hiện tại. Sau đó nếu bước đi tiếp theo là Stop nghĩa là đó là tường thì ta sẽ trả về giá trị âm vô cùng => pacman sẽ không đi bước đó. Nếu bước đi đó không phải tường thì ta sẽ kiểm tra xem liệu vị trí tiếp theo có gặp con ma hay không, và khi đó thời gian con ma sợ có còn không. Nếu bước đi tiếp theo gặp con ma và con ma không sợ thì trả về âm vô cùng => pacman không đi nước này. Còn nếu vị trí tiếp theo không gặp ma và tường thì chúng ta sẽ trả về giá trị âm của khoảng cách đến thức ăn gần nhất vì khi đó những nước đi có khoảng cách đến thức ăn gần hơn sẽ có giá trị lớn hơn.
 - Question 2: 
    + Đầu tiên ta sẽ có hàm isEnd để kiểm tra trạng thái kết thúc của hàm đệ quy, hàm này kết thúc khi thua, thắng hoặc khi duyệt đủ độ sâu.
    + Hàm findMin để tìm ra giá trị nhỏ nhất có thể của state khi ghost thực hiện các hành động. Nếu là state kết thúc sẽ trả về giá trị của state qua hàm evaluationFunction. Nếu chưa kết thúc thì ta sẽ xét từng hành động của một con ma, tính giá trị state của khi các từng ma hành động và trả về giá trị nhỏ nhất của chúng. Khi đã xét đến hành động của con ma cuối cùng, chúng ta sẽ thực hiện duyệt đến độ sâu tiếp theo bằng cách gọi findMax để xét hành động của pacman ở độ sâu tiếp theo.
    + Hàm findMax để tìm giá trị lớn nhất có thể của state khi pacman thực hiện các hành động. Nếu là state kết thúc sẽ trả về giá trị của state qua evaluationFunction. Nếu chưa kết thúc thì ta sẽ xét từng hành động của pacman, lấy giá trị lớn nhất của state qua từng hành động của pacman bằng cách gọi lại hàm findMin để xét tiếp hành động của các con ma ở độ sâu này.
    + Như vậy đây là một hàm đệ quy với trạng thái kết thúc là thua, thắng hoặc duyệt đủ độ sâu. Ban đầu duyệt ở độ sâu 0 với hành động của pacman bằng findMax, sau đó tiếp tục duyệt ở độ sâu 0 với hành động của các con ma bằng findMin. Tiếp tục như vậy đến các độ sâu tiếp theo sẽ tính được giá trị của state khi thực hiện 1 hành động rồi tìm ra hành động làm state có giá trị lớn nhất.
 - Question 3: Tương tự câu trên tuy nhiên ở đây chúng ta sẽ có thêm 2 biến khi duyệt cây đó là alpha để lưu giá trị nhỏ nhất đã tìm được và beta để lưu giá trị lớn nhất đã tìm được ở một độ sâu. 
    + Nếu ở trong hàm findMax mà hàm findMin trong nó tìm được một giá trị hành động bất kỳ nhỏ hơn beta thì hàm findMin đó sẽ không cần thực hiện tiếp, nếu vẫn tìm thấy các giá trị lớn hơn beta thì  sẽ gán beta bằng nó và thực hiện tiếp hàm findMin để tìm ra giá trị min lớn nhất cho hàm findMax.
    + Tương tự nếu ở trong hàm findMin mà hàm findMax trong nó tìm được một giá trị hành động bất kỳ lớn hơn alpha thì hàm findMax đó sẽ không cần thực hiện tiếp, nếu vẫn tìm thấy các giá trị nhỏ hơn alpha thì sẽ gán alpha bằng giá trị đó và thực hiện tiếp findMax để tìm ra giá trị max nhỏ nhất cho hàm findMin.
