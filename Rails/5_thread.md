# Thread trong Ruby

- Thread (luồng) là một đơn vị thực thi cơ bản trong một chương trình. Nó cho phép chương trình thực hiện nhiều công việc đồng thời, bằng cách chia nhỏ quá trình thực thi thành nhiều luồng có thể chạy song song. Trong Ruby, Thread là một lớp cung cấp khả năng tạo và quản lý các luồng.

## Đặc điểm của Thread

- Đồng thời (Concurrency): Các luồng cho phép thực thi đồng thời nhiều phần của chương trình. Điều này không nhất thiết phải là song song, nhưng cho phép các tác vụ độc lập tiến hành đồng thời, chia sẻ tài nguyên CPU.

- Độc lập: Mỗi luồng có thể thực thi độc lập và không phụ thuộc vào luồng khác. Điều này có nghĩa là các luồng có thể chạy và hoàn thành mà không chặn hoặc cản trở luồng chính của chương trình.

- Chia sẻ tài nguyên: Các luồng trong cùng một quá trình chia sẻ cùng không gian địa chỉ, bao gồm bộ nhớ và tài nguyên hệ thống. Điều này có thể tạo ra các vấn đề về đồng bộ hóa nếu không được quản lý đúng cách.

Ví dụ :

```
def task(name, duration)
  puts "#{name} started"
  sleep(duration)
  puts "#{name} completed"
end

# Tạo và khởi chạy các luồng
thread1 = Thread.new { task("Task 1", 2) }
thread2 = Thread.new { task("Task 2", 3) }
thread3 = Thread.new { task("Task 3", 1) }

# Đợi tất cả các luồng hoàn thành
[thread1, thread2, thread3].each(&:join)

puts "All tasks completed"
```

## Lợi ích của việc sử dụng Thread

- Hiệu suất: Sử dụng luồng có thể cải thiện hiệu suất bằng cách thực hiện đồng thời nhiều công việc, đặc biệt là khi các công việc này không phụ thuộc vào nhau và có thể chạy song song.

- Tăng khả năng đáp ứng: Bằng cách thực hiện các tác vụ tốn thời gian trong các luồng riêng, chương trình có thể phản hồi nhanh hơn đối với các yêu cầu của người dùng.

- Sử dụng tài nguyên hiệu quả: Luồng cho phép sử dụng CPU và các tài nguyên hệ thống khác một cách hiệu quả hơn bằng cách chia sẻ tải công việc.

## Vấn đề cần lưu ý khi sử dụng Thread

- Đồng bộ hóa: Khi nhiều luồng truy cập cùng một tài nguyên (chẳng hạn như biến hoặc đối tượng), cần phải quản lý sự đồng bộ để tránh xung đột và bảo đảm tính nhất quán của dữ liệu.

- Deadlock: Deadlock xảy ra khi hai hoặc nhiều luồng chờ đợi lẫn nhau để giải phóng tài nguyên, dẫn đến tình trạng dừng hoàn toàn.

- Chi phí quản lý: Quản lý luồng và đồng bộ hóa có thể làm tăng độ phức tạp của mã và gây khó khăn trong việc gỡ lỗi.

## Kết luận

- Sử dụng Thread trong Ruby có thể mang lại nhiều lợi ích về hiệu suất và khả năng đáp ứng, nhưng cũng đòi hỏi phải quản lý đúng cách để tránh các vấn đề về đồng bộ hóa và deadlock. Ví dụ trên minh họa cách tạo và sử dụng luồng để thực hiện các tác vụ đồng thời mà không chặn luồng chính của chương trình.

---------------

### Deadlock là gì?

- Deadlock (khóa chết) là một tình trạng trong hệ thống máy tính khi hai hoặc nhiều tác vụ (hoặc luồng) không thể tiếp tục hoạt động vì mỗi tác vụ đang chờ một tài nguyên mà một tác vụ khác đang giữ. Điều này tạo ra một vòng lặp không có hồi kết, khiến tất cả các tác vụ liên quan bị chặn và không thể tiến hành thêm được nữa.

- Ví dụ về Deadlock

  + Giả sử chúng ta có hai luồng (thread) và hai tài nguyên (resource):

    + Thread 1 cần Resource A và Resource B để hoàn thành công việc.

    + Thread 2 cũng cần Resource A và Resource B để hoàn thành công việc.

  + Quá trình xảy ra deadlock:

    + Thread 1 chiếm Resource A và yêu cầu Resource B.

    + Thread 2 chiếm Resource B và yêu cầu Resource A.

    + Cả hai luồng đều bị chặn vì:

      + Thread 1 đang giữ Resource A nhưng chờ Resource B (đang bị Thread 2 giữ).

      + Thread 2 đang giữ Resource B nhưng chờ Resource A (đang bị Thread 1 giữ).

  + Cả hai luồng không thể tiến lên hoặc giải phóng tài nguyên mà chúng đang giữ, dẫn đến deadlock.

  ```
  mutex_a = Mutex.new
  mutex_b = Mutex.new

  Thread.new do
    mutex_a.synchronize do
      sleep(1) # Giả lập thời gian chờ
      mutex_b.synchronize do
        puts "Thread 1 đã chiếm cả Resource A và Resource B"
      end
    end
  end

  Thread.new do
    mutex_b.synchronize do
      sleep(1) # Giả lập thời gian chờ
      mutex_a.synchronize do
        puts "Thread 2 đã chiếm cả Resource B và Resource A"
      end
    end
  end

  sleep(2)
  ```
