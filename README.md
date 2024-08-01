### UC-01: Thay đổi hạn mức trên Web/ App (MAMO.1)



### Cầm cố

#### UC-02: Cầm cố web/ app (MAMO.2)

#### UC-08: Cầm cố internal (MAMO.8)

- b1: Check RequestId tại Log Input Memory

- b2: Gọi SP Validate (trong SP có ghi Log Input DB)
  - Exception gọi SP Validate Fail -> Gửi Pusher
- b3: Ghi Log Input Memory
- b4: Gửi Msg CK sang topic Account
- b5: Nhận phản hồi CK Account
  - Check xem Log Input Memory đã được ghi chưa
  - Update Log Input Memory
  - Exception nhận phản hồi CK Fail 
    - Check xem Log Input Memory đã được ghi chưa
    - Update Log Input (memory + DB)
    - Gửi Pusher
- b6: Gửi Msg Tiền sang topic Account
- b7: Nhận phản hồi Tiền Account
  - Check xem Log Input Memory đã được ghi chưa
  - Update Log Input Memory
  - Exception nhận phản hồi Tiền Fail
    - Check xem Log Input Memory đã được ghi chưa
    - Update Log Input (memory + DB)
    - Gửi Pusher
- b8: Gọi SP làm nghiệp vụ cầm cố và update Log Input DB
  - Exception gọi SP làm nghiệp vụ Fail
    - Gửi Msg Revert CK Account
    - Gửi Msg Revert Tiền Account
    - Gửi Pusher
- b9: Gọi SP cập nhật TRD
  - Exception gọi SP Fail -> chỉ ghi Log
- b10: Gửi Msg sang topic Output Mamo
- b11: Gửi Pusher 



### Trả nợ

#### UC-03: Trả nợ web/ app (MAMO.3)

- b1: Check RequestId tại Log Input Memory
- b2: Gọi SP Validate (trong SP có ghi Log Input DB)
  - Exception gọi SP Validate Fail -> Gửi Pusher
- b3: Ghi Log Input Memory
- b4: Gửi Msg Tiền sang topic Account
- b5: Nhận phản hồi Tiền Account
  - Check Log Input Memory xem đã ghi chưa
  - Update Log Input (memory + DB)
  - Exception nhận phản hồi Tiền Fail
    - Check Log Input Memory xem đã ghi chưa
    - Update Log Input (memory+DB)
    - Gửi Pusher
- b6: Gửi msg CK sang topic Account
- b7: Nhận phản hồi CK Account
  - Check Log Input Memory xem đã ghi chưa
  - Update Log Input Memory 
  - Exception nhận phản hồi CK Account Fail 
    - Check Log Input Memory xem đã ghi chưa
    - Update Log Input (memory + DB)
    - Gửi Msg Revert Tiền sang topic Account
    - Gửi Pusher
- b8: Gọi SP làm nghiệp vụ trả nợ và update lại Log Input DB
  - Exception gọi SP làm nghiệp vụ Fail
    - Gửi Msg Revert Tiền sang topic Account
    - Gửi Msg Revert CK sang topic Account
    - Gửi Pusher
- b9: Gọi SP cập nhật TRD
  - Exception gọi SP lỗi -> chỉ ghi Log
- b10: Gửi Msg sang topic Output Mamo
- b11: Gửi Pusher



#### UC-09: Trả nợ internal (MAMO.9)





### Gia hạn

#### UC-04: Gia hạn web/ app (MAMO.4)

- b1: Check RequestId tại Log Input Memory
- b2: Gọi SP Validate (trong SP có ghi Log Input DB)
  - Exception gọi SP Validate Fail -> Gửi Pusher
- b3: Ghi Log Input Memory
- b4: Gửi Msg Tiền sang topic Account
- b5: Nhận phản hồi Tiền Account
  - Check Log Input Memory xem đã ghi chưa
  - Update Log Input Memory
  - Exception nhận phản hồi Tiền Account Fail
    - Check Log Input Memory xem đã ghi chưa
    - Update Log Input (memory + DB)
    - Gửi Pusher
- b6: Gọi SP làm nghiệp vụ Gia hạn (trong SP có update Log Input DB)
  - Exception gọi SP làm nghiệp vụ Fail
    - Gửi Msg Revert Tiền sang topic Account
    - Gửi Pusher
- b7: Gọi SP cập nhật TRD
  - Exception gọi SP Fail -> chỉ ghi Log
- b8: Gửi Msg sang topic Output Mamo
- b9: Gửi Pusher



#### UC-10: Gia hạn internal (MAMO.10)

- b1: Check RequestId tại Log Input Memory
- b2: Gọi SP Validate (trong SP có ghi Log Input DB)
  - Exception gọi SP Validate Fail -> Gửi Pusher
- b3: Ghi Log Input Memory
- b4: Gửi Msg Tiền sang topic Account
- b5: Nhận phản hồi Tiền Account
  - Check Log Input Memory xem đã ghi chưa
  - Update Log Input Memory
  - Exception nhận phản hồi Tiền Account Fail 
    - Check Log Input Memory xem đã ghi chưa
    - Update Log Input (memory+DB)
    - Gửi Pusher
- b6: Gọi SP làm nghiệp vụ Gia hạn (trong SP có update Log Input DB)
  - Exception gọi SP làm nghiệp vụ Fail
    - Gửi Msg Revert Tiền sang topic Account
    - Gửi Pusher
- b7: Gọi SP cập nhật TRD
  - Exception gọi SP cập nhật TRD -> chỉ ghi Log
- b8: Gửi Msg Output Mamo
- b9: Gửi Pusher



### UC-05: Đăng ký dịch vụ Mamo (MAMO.5)



### UC-06: Hủy dịch vụ Mamo (MAMO.6)



### UC-07: Phân bổ quyền (MAMO.7)

- b1: Check RequestId tại Log Input Memory
- b2: Gọi SP làm nghiệp vụ bổ quyền và Log Input cho ALL row (lỗi 1 dòng update Log Input và xử lý tiếp các dòng khác)
- b3: Gọi SP lấy danh sách cần gửi Account (chỉ lấy các dòng đã xử lý thành công ở DB và chưa gửi Account)
- b4: Ghi Log Input Memory
- b5: Ghi Log Sum Memory
- b6: Gửi Msg Tiền sang topic Account cho ALL row 
- b7: Nhận phản hồi Tiền Account
  - Check Log Input Memory xem đã ghi chưa
  - Update Log Input Memory
  - Exception nhận phản hồi Tiền Account Fail
    - Check Log Input Memory xem đã ghi chưa
    - Update Log Input Memory
    - Update Log Sum Memory
    - Check Log Sum (nếu đã nhận đủ phản hồi Account thì)
      - Update Log Input, Log Sum DB
      - Gửi Msg Output Mamo (gọi SP để lấy DS)
      - Gửi Mail kết quả cho user, FIT
- b8: Gửi Msg CK sang topic Account
- b9: Nhận phản hồi CK Account
  - Check Log Input Memory xem đã ghi chưa
  - Update Log Input Memory 
  - Update Log Sum Memory
  - Check Log Sum (nếu đã nhận đủ phản hồi Account thì):
    - Update Log Input, Log Sum vào DB
    - Gửi Msg Output Mamo (gọi SP để lấy danh sách)
    - Gửi Mail kết quả cho user, FIT
  - Exception nhận phản hồi CK Account Fail
    - Check Log Input Memory xem đã ghi chưa
    - Update Log Input Memory 
    - Update Log Sum Memory 
    - Gửi Msg Revert Tiền sang topic Account 
    - Check Log Sum (nếu đã nhận đủ phản hồi Account thì)
      - Update Log Input, Log Sum DB
      - Gửi Msg Output Mamo (gọi SP để lấy DS)
      - Gửi Mail kết quả cho User, FIT
  - Exception Service khởi động lại
    - Check Log Sum: Lấy số Msg cần gửi Tiền, CK Account
    - Check với Account xem nhận được bao nhiêu Msg Tiền, CK
    - Update Log Sum, Log Input để chạy lại API hoặc SV tự chạy tiếp
    - Gửi tay Msg thiếu


### UC-11: Cầm cố quyền (MAMO.11)
> - Thuộc nghiệp vụ cuối ngày (sv endday)
> - Tăng dư nợ, giảm CK mar
> - Gửi Account msg Tiền trước, CK sau
> - Xử lý trước, nhận phản hồi sau
> - Account không check số dư

- b1: Gọi SP validate **spmamo_mor_rights_validate** (check trạng thái Job đang bật, check ngày nghỉ, ...)
- b2: Gọi API **http://rightoltpgtw-dev.securities.fpts.com.vn:8086/api/v1/RightOltp/rightformort-list** lấy danh sách thông tin quyền từ Custd
- b3: Gọi SP **spmamo_mor_rights** làm nghiệp vụ cầm cố quyền. Xử lý và Log Input DB cho ALL row (lỗi 1 dòng thì update log input db và xử lý tiếp các dòng khác)
- b4: Gọi SP lấy danh sách cần gửi Account (lấy các dòng xử lý thành công ở DB để gửi Account)
  - Log Input Memory
  - Log Sum Memory
- b5: Gửi msg Tiền sang topic Account **Information.Account.Cash**
- b6: Nhận phản hồi msg topic Output Tiền Account **Information.Account.Cash.Output**
  - Check log input memory
  - Update log input memory
  - Exception nhận phản hồi msg Tiền từ Acc Fail
    - Check log input memory
    - Update log input memory
    - Update log sum memory
    - Check log sum: Nếu đã nhận đủ phản hồi Account rồi thì
      - Update log input db, log sum db
      - Gọi sp để lấy danh sách dư liệu gửi topic Output Mamo
      - Gọi SP cập nhật TRD 
      - Exception gọi sp cập nhật trd fail -> chỉ ghi log và chạy tiếp
      - Gửi mail kết quả cho user, Fit (mail Fit ghi rõ bao nhiêu dòng lỗi ở DB, bao nhiêu dòng lỗi ở Account)
- b7: Gửi msg CK sang topic Account
- b8: Nhận phản hồi CK topic Account
  - Check log input memory
  - Update log input memory
  - Update log sum memory 
  - Check log sum: Nếu đã nhận đủ phản hồi msg từ Account rồi thì 
    - Update log input db, log sum db
    - Gọi SP để lấy danh sách gửi msg ra topic Output Mamo
    - Gọi SP cập nhật TRD
    - Exception gọi sp cập nhật trd fail -> chỉ ghi log và chạy tiếp
    - Gửi mail kết quả cho user, Fit (mail Fit ghi rõ bao nhiêu dòng lỗi ở DB, bao nhiêu dòng lỗi ở Account)
  - Exception nhận phải hồi msg CK Account Fail thì
    - Check log input memory
    - Update log input memory
    - Update log sum memory
    - Gửi msg revert Tiền sang Account
    - Check log sum: Nếu đã nhận đủ phản hồi Accout thì:
      - Update log input db, log sum db
      - Gọi SP để lấy danh sách dữ liệu gửi ra topic Output Mamo
      - Gọi SP cập nhật TRD
      - Gửi mail kết quả cho user, Fit (mail Fit ghi rõ bao nhiêu dòng lỗi ở db, bao nhiêu dòng lỗi ở Account)
- Service khởi động lại 
  - Check log sum: lấy số msg cần gửi Tiền, CK account
  - Check với Account xem nhận được bao nhiêu Msg Tiền, Ck
  - Update log input, log sum để chạy lại api hoặc sv tự chạy tiếp
  - Gửi tay msg thiếu


### UC-12: Gia hạn tự động hợp đồng T+ (MAMO.12)

> - Thuộc nghiệp vụ cuối ngày (sv endday)
> - Tăng dư nợ 
> - Gửi Account msg Tiền
> - Xử lý trước, nhận phản hồi Account sau
> - Account không check số dư

- b1: Gọi SP validate **spmamo_extendadd_auto_validate** (check trạng thái bật job, check ngày nghỉ, ...)

- b2: Lấy thông tin phương thức xử lý HĐ từ Fee: Gọi API lấy danh sách **http://para.fee.rs-dev.toms.fpts.com.vn:8086/api/v1/fee/method-margin**

- b2: Gọi SP làm nghiệp vụ **spmamo_extendadd_auto** gia hạn tự động hđ T+ để xử lý và log input cho ALL row (lỗi 1 dòng thì update log input db và xử lý tiếp các dòng khác)

- b3: Lấy danh sách gửi noti cho KH (rs3 của sp nghiệp vụ) ra topic **Utility.Notification.MessageSendRequest**

- b4: Lấy danh gửi msg sang topic Account (chỉ lấy các dòng đã xử lý thành công ở DB và chưa gửi Account) (rs1 của sp nghiệp vụ)

  - Log input memory
  - Log sum memory

- b5: Gửi msg Tiền sang topic Account **Information.Account.Cash**

- b6: Nhận phản hồi Tiền từ topic Output Account **Information.Account.Cash.Output**

  - Check log input memory

  - Update log input memory

  - Update log sum memory

  - Check log sum: nếu đã nhận đủ phản hồi Account thì 

    - Update log input db, log sum db

    - Gọi sp **spmamo_extendadd_auto_get** lấy danh sách dữ liệu để gửi topic Output Mamo **Loans.Mamo.Output**

    - Gửi **Mail** kết quả cho user, fit (mail fit ghi rõ bao nhiêu dòng lỗi ở db, bao nhiêu dòng lỗi ở Acocunt)
  - Exception nhận phản hồi msg Tiền Account Fail thì:
    - Check log input memory
    - Update log input memory
    - Update log sum memory
    - Check log sum: nếu đã nhận đủ phản hồi Account thì
      - Update log input db, log sum db
      - Gọi sp để lấy danh sách dữ liệu gửi topic Output Mamo
      - Gửi mail kết quả cho user, fit (mail fit ghi rõ bao nhiêu dòng lỗi ở db, bao nhiêu dòng lỗi ở Account)



### UC-13: Cập nhật trạng thái thị trường (MAMO.13)

> - Thuộc nghiệp vụ cuối ngày (sv endday)
> - Không gửi msg sang Account

b1: Gọi Sp cập nhật trạng thái thị trường

b2: Nếu đầu vào API MarketState=1 thì gọi thêm sp cập nhật danh sách các hợp đồng không được trả nợ


### Tạo hợp đồng Margin
  - API Tìm kiếm DS HĐ Margin cần tạo **http://mamo.rs-dev.loans.fpts.com.vn:8086/api/v1/Margin/contracts/NAMNV**

```
Tạo hợp đồng T+
b1: vào eztrade đặt lệnh mua Ký quỹ (TK phải đc đk T+)
b2: nhờ Loan khớp lệnh
b3: nhờ Thảo SST đẩy trade về nova
b4: vào form tạo hợp đồng marign tổng hợp rồi tạo hđ


Thay đổi hạn mức trên eztrade/mobile
vào thay đổi, nếu phải duyệt thì vào hạn mức trên ezmargin để duyệt
nếu người duyệt có hạn mức nhỏ hơn hạn mức duyệt thì phải qua form duyệt quản lý rủi ro 

```


#### UC-14: Tổng hợp Trade mua Margin (để tạo HĐ Margin) (MAMO.14)

> - Thuộc nghiệp vụ cuối ngày (sv endday)
> - Không gửi msg sang topic Account

- b1: Gọi API nova để lấy danh sách trade mua margin trong ngày
- b2: Gọi sp mamo **spmamo_mar_create_sum** để insert dữ liệu vào db
  - Exception gọi sp mamo fail thì api phản hồi false, code, msg lỗi

- API Tổng hợp Trade mua Margin (để tạo HĐ margin) **http://endday.mamo.sv-dev.loans.fpts.com.vn:8086/api/v1/Mamo/buy**


#### UC-15: Tạo HĐ Margin (MAMO.15)

> - Thuộc nghiệp vụ cuối ngày (sv endday)
> - Tăng dư nợ
> - Gửi msg Tiền sang topic Account
> - Xử lý trước, nhận phản hồi Account sau
> - Account không check số dư

- API Tạo hợp đồng Margin **http://endday.mamo.sv-dev.loans.fpts.com.vn:8086/api/v1/Mamo**
- b1: Check RequestId tại Log Input Memory
- b2: Gọi API Fee để lấy danh sách tài khoản đang dùng T+
- b3: Gọi SP làm nghiêp vụ tạo hợp đồng để xử lý và log input cho ALL row (lỗi 1 dòng thì update log input db và xử lý tiếp các dòng khác)
- b4: Gọi SP lấy danh sách cần gửi msg sang topic Account (chỉ lấy các dòng đã xử lý thành công ở DB và chưa gửi Account)
  - Log input memory
  - Log sum memory
- b5: Gửi msg Tiền sang topic Account cho ALL row
- b6: Nhận phải hồi Tiền từ topic Account:
  - Check log input memory
  - Update log input memory
  - Update log sum memory
  - Check log sum: nếu đã nhận đủ phản hồi Account rồi thì:
    - Update log input db, log sum db
    - Gọi sp lấy danh sách dữ liệu để gửi msg ra topic Output Mamo
    - Gửi Pusher
  - Exception nhận phản hồi tiền Account Fail
    - Check log input memory
    - Update log input memory
    - Update log sum memory
    - Check log sum : nếu đã nhận đủ phản hồi Account rồi thì
      - Update log input db, log sum db
      - Gọi SP để lấy danh sách dữ liệu để gửi topic Output Mamo
      - Gửi Pusher

### UC-16: Tổng hợp Trade bán Margin (để PI Margin) (MAMO.16)





### UC-17: Tạo GD trả nợ bằng bán ký quỹ PI (MAMO.17)





### UC-18: Cập nhật giá tham chiếu (để cập nhật hđ mamo khi chạy hệ thống) (MAMO.18)



### UC-19: Cập nhật HĐ mamo khi chạy HT (MAMO.19)





### UC-20: Cập nhật giá sàn (khi tổng hợp các HĐ bị thanh lý và khi EOD) (MAMO.20)







### UC-21: Tổng hợp các HĐ bị thanh lý (MAMO.21)





### UC-22: Xóa HĐ mamo bị thanh lý (MAMO.22)



### UC-23: Settle trả nợ bằng bán ký quỹ (MAMO.23)



### UC-24: Cập nhật tham số Mamo cho từng TK (MAMO.24)



### UC-25: Cập nhật tham số Mamo cho ALL KH (MAMO.25)



### UC-26: Cập nhật tham số phí HTV cho ALL KH (MAMO.26)



### UC-27: Đối chiếu PI (MAMO.27)



### UC-28: Đối chiếu hợp đồng Mamo (MAMO.28)



### UC-29: Đối chiếu trả nợ Mamo (MAMO.29)



### UC-30: Thông báo cho KH các HĐ Mamo quá hạn (MAMO.30)



### UC-31: Thông báo trạng thái HĐ (tất toán/ rơi vào mức xử lý) Mamo (MAMO.31)











