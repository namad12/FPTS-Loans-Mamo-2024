> [LoansMamo.Api Service](http://mamo.rs-dev.loans.fpts.com.vn:8086/swagger/index.html)
> 
> [LoansMamo.Intraday Service](http://intraday.mamo.sv-dev.loans.fpts.com.vn:8086/swagger/index.html)
> 
> [LoansMamo.Endday Service](http://endday.mamo.sv-dev.loans.fpts.com.vn:8086/swagger/index.html)
> 
> [MamoMailService](http://mail.mamo.sv-dev.loans.fpts.com.vn:8086/swagger/index.html)


# EzLoans
## Giao dịch > Margin 
### Form: Cầm cố CK

### Form: Trả nợ Mamo

### Form: Gia hạn HĐ Mamo

## Chạy hệ thống > Margin
### Form: 1. Trạng thái thị trường Mamo

### Form: 2. Tạo hợp đồng Margin

### Form: 3. PI Mamo

### Form: 4. Cập nhật hợp đồng Mamo

### Form: 5. Xóa hợp đồng thanh lý Mamo

### Form: Đối chiếu PI

### Form: Đối chiếu HĐKQ

### Form: Đối chiếu GDTNKQ

### Form: Xóa bán xử lý Margin thường theo danh sách

### Form: Lùi giờ Mamo

## Báo cáo > Margin
### Form: Tra cứu số dư Mamo

### Form: Tra cứu hợp đồng Mamo

### Form: Tra cứu trả nợ Mamo

### Form: Tra cứu trả nợ từ bán CK

### Form: In hợp đồng trả nợ Mamo

### Form: Tra cứu gia hạn Mamo

### Form: Tra cứu tình trạng hợp đồng

### Form: Danh sách xử lý T-1 chưa trả nợ

### Tra cứu bán xử lý Mamo

### [Kiểm soát phiếu lệnh ký quỹ](https://internal.fpts.com.vn/EzLoans/Pages/BaoCao/Margin/KiemSoatPhieuLenh.aspx) (FRM và AST dùng)
#### [Popup Broker đặt lệnh](https://internal.fpts.com.vn/EzLoans/Pages/BaoCao/Margin/Popup/BrokerPopup.aspx) (icon Kính lúp)
- Gọi API bên Fee để lấy thông tin Broker **http://para.fee.rs-dev.toms.fpts.com.vn:8086/api/v1/fee/broker-actvice?** (input: brokerid, brokername)
#### Mã khách hàng 058C TextOnchanged thì hiện nút Người Ủy quyền
- Gọi API bên EzOpen để lấy thông tin KH **http://ezopengtw-dev.customer.fpts.com.vn:8086/api/v1/Ezopen/customerinfo-by-client?Custaccount=** (input: 058C292589)
#### Lấy thông tin Ủy quyền KH (bấm nút Người UQ)
- Gọi API bên EzOpen để lấy thông tin Ủy quyền KH **http://ezopengtw-dev.customer.fpts.com.vn:8086/api/v1/Ezopen/authorizedcust_get?clientcode=** (input: 058C292589)
#### Tìm kiếm
- Gọi API trong service LoansMamo.Api **http://mamo.rs-dev.loans.fpts.com.vn:8086/api/v1/Margin/checking-order?** (input: fromDate, toDate, clientCode, broker, type, agentGroup, status)
- API gọi vào sp **spmamo_checkingorder_get**
#### Cập nhật Trạng thái phiếu
- Gọi API method PUT service LoansMamo.Eod **http://endday.mamo.sv-dev.loans.fpts.com.vn:8086/checking-order** (input: id, status, note, date, user)
- API gọi vào SP **spmamo_checkingorder_u** để cập nhật trạng thái phiếu
#### Cập nhật Note
- Gọi API method PUT service LoansMamo.Eod **http://endday.mamo.sv-dev.loans.fpts.com.vn:8086/checking-order** (input: id, status, note, date, user)
- API gọi vào SP **spmamo_checkingorder_u** để cập nhật Note
#### Tổng hợp (chỉ được tổng hợp sau 16h30)
- Gọi API method POST service LoansMamo.Eod **http://endday.mamo.sv-dev.loans.fpts.com.vn:8086/checking-order** (input: transDate)
- API gọi vào SP **spmamo_checkingorder_i** để cập nhật Note

### [Tra cứu phiếu lệnh](https://internaluat.fpts.com.vn/EzLoans/Pages/BaoCao/Margin/SearchOrderSlips.aspx) (FRM và AST dùng)
#### [Popup Broker đặt lệnh](https://internal.fpts.com.vn/EzLoans/Pages/BaoCao/Margin/Popup/BrokerPopup.aspx) (icon Kính lúp)
- Gọi API bên Fee để lấy thông tin Broker **http://para.fee.rs-dev.toms.fpts.com.vn:8086/api/v1/fee/broker-actvice?** (input: brokerid, brokername)
#### Mã khách hàng 058C TextOnchanged thì hiện nút Người Ủy quyền
- Gọi API bên EzOpen để lấy thông tin KH **http://ezopengtw-dev.customer.fpts.com.vn:8086/api/v1/Ezopen/customerinfo-by-client?Custaccount=** (input: 058C292589)
#### Tìm kiếm
- Gọi API trong service LoansMamo.Api **http://mamo.rs-dev.loans.fpts.com.vn:8086/api/v1/Margin/checking-order?** (input: fromDate, toDate, clientCode, broker, type, agentGroup, status)
- API gọi vào sp **spmamo_checkingorder_get**
























































































### UC-01: Thay đổi hạn mức trên Web/ App (MAMO.1)

### Cầm cố trên Internal, EzTrade, Mobile

#### UC-02: Cầm cố web/ app (MAMO.2)
> - Thuộc nghiệp vụ trong ngày (sv intraday)
> - Api xử lý cho 1 row
> - Tăng tiền, giảm CK
> - Gửi message sang Account topic CK trước, Tiền sau
> - Nhận phản hồi Account thì mới xử lý tiếp

- Check RequestId tại InputLog trong Memory xem có không
  - Nếu có thì return **Already processing request ...** và kết thúc API
- Gọi SP **spmamo_mortgageadd_validate_eztrade** để Validate
- Nếu SP validate Fail thì return kết thúc API
- Nếu thành công thì lấy dữ liệu RS trả về từ SP **spmamo_mortgageadd_validate_eztrade** lưu vào InputLog Memory
  - Gọi hàm HandleLogic xử lý tiếp
    - Gửi message CK sang topic Account ****
  - Nếu hàm xử lý Fail thì xóa InputLog memory sau đó return và kết thúc API
    

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
> - Thuộc nghiệp vụ trong ngày

- b1: Gọi SP làm nghiệp vụ đăng ký dịch vụ mamo **spmamo_paramfromezopen_i_acc3**
  - Nếu Thành công thì
    - Insert log vào sp **spmarp_status_msg_acc**
      - SP return Done thì -> Gửi message tiền sang topic Account **Information.Account.Cash** -> Return API **Chờ xử lý**
      - SP return Fail thì -> Gửi message thất bại ra topic output **Loans.Mamo.Output** -> Return API **Lỗi xử lý**
  - Nếu SP return Fail thì Gửi msg ra topic pusher ezopen **Loans.Mamo.Output** -> Return API **Lỗi xử lý**
- b2: Nhận phản hồi từ topic output **Information.Account.Cash.Output** từ account
  - Nếu acc phản hồi thành công thì -> Gửi message Thành công ra topic output **Loans.Mamo.Output, Information.Parameter.Mamo.Output**
  - Nếu acc phản hồi thất bại thì
    - Gọi SP revert lại nghiệp vụ đăng ký dịch vụ mamo **spmamo_paramfromezopen_r_acc3**
    - Gửi message Thất bại ra topic output **Loans.Mamo.Output**


### UC-06: Hủy dịch vụ Mamo (MAMO.6)
> - Thuộc nghiệp vụ trong ngày

- b1: Gọi SP insert log **spmarp_status_msg_acc**
  - Nếu SP return Success thì -> Gửi message tiền sang topic Account **Information.Account.Cash** -> Return API **Chờ xử lý**
  - Nếu SP return Fail thì -> Gửi message thất bại ra topic output **Loans.Mamo.Output** -> Return API **Lỗi xử lý**
- b2: Nhận phản hồi từ topic output **Information.Account.Cash.Output** từ account
  - Nếu acc phản hồi thành công thì -> Gọi SP làm nghiệp vụ hủy đăng ký dịch vụ mamo **SPMAMO_PARAMFROMEZOPEN_CLOSE**
    - Nếu SP return Success thì -> Gửi message Thành công ra topic output **Loans.Mamo.Output, Information.Parameter.Mamo.Output**
    - Nếu SP return Fail thì -> Gửi message Revert Tiền ra topic account, và topic output cho ezopen **Information.Account.Cash, Loans.Mamo.Output**
  - Nếu acc phản hồi thất bại thì -> Gửi message thất bại ra topic cho ezopen **Loans.Mamo.Output**
     
### Phân bổ quyền (MAMO.7)
#### UC-07: Phân bổ quyền (MAMO.7)
> - Thuộc nghiệp vụ trong ngày (service intraday)
> - API xử lý cho N row
> - Tăng dư nợ, tăng CK mar
> - Gửi message account ra topic tiền trước, message chứng khoán sau
> - Xử lý trước, nhận phản hồi account sau

- b1: Check RequestId tại Log Input Memory
- b2: Gọi SP **spmamo_distribute_mor_rights** làm nghiệp vụ bổ quyền và trong SP Log Input cho ALL row (lỗi 1 dòng update Log Input và xử lý tiếp các dòng khác)
- b3: Lấy danh sách **RS1** cần gửi Account (chỉ lấy các dòng đã xử lý thành công ở DB và chưa gửi Account) trong SP **spmamo_distribute_mor_rights**
- b4: Ghi Log Input Memory
- b5: Ghi Log Sum Memory
- b6: Gửi Msg Tiền sang topic Account **Information.Account.Cash** cho ALL row 
- b7: Nhận phản hồi Tiền Account từ topic **Information.Account.Cash.Output**
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
- b8: Gửi Msg CK sang topic Account **Information.Account.Securities** cho ALL row
- b9: Nhận phản hồi CK Account từ topic **Information.Account.Securities.Output**
  - Check Log Input Memory xem đã ghi chưa
  - Update Log Input Memory 
  - Update Log Sum Memory
  - Check Log Sum (nếu đã nhận đủ phản hồi Account thì):
    - Update Log Input, Log Sum vào DB
    - Gửi Msg Output Mamo (gọi SP **spmamo_distribute_mor_rights_get** để lấy danh sách)
    - Gọi SP **sptrd_distribute_exec** cập nhật TRD
      - Exception: Gọi SP TRD lỗi thì vẫn làm tiếp nghiệp vụ
    - Gửi Mail kết quả cho user, FIT
  - Exception nhận phản hồi CK Account Fail
    - Check Log Input Memory xem đã ghi chưa
    - Update Log Input Memory 
    - Update Log Sum Memory 
    - Gửi Msg Revert Tiền sang topic Account 
    - Check Log Sum (nếu đã nhận đủ phản hồi Account thì)
      - Update Log Input, Log Sum DB
      - Gửi Msg Output Mamo (gọi SP **spmamo_distribute_mor_rights_get** để lấy DS)
      - Gọi SP **sptrd_distribute_exec** cập nhật TRD
        - Exception: Gọi SP TRD lỗi thì vẫn làm tiếp nghiệp vụ
      - Gửi Mail kết quả cho User, FIT
  - Exception Service khởi động lại
    - Check Log Sum: Lấy số Msg cần gửi Tiền, CK Account
    - Check với Account xem nhận được bao nhiêu Msg Tiền, CK
    - Update Log Sum, Log Input để chạy lại API hoặc SV tự chạy tiếp
    - Gửi tay Msg thiếu
   
#### UC-07: Check số HĐ ccq có mã ck không còn trong danh mục cho vay - ezcust gọi để bổ quyền (MAMO.7)
> - Thuộc Service LoansMamo.Api
> - Api check **http://mamo.rs-uat.loans.fpts.com.vn:8086/api/v1/Mortgage/MorRight-Check**
> - Api gọi tới SP Mamo **spmamo_mor_rights_check**


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



### UC-13: [Cập nhật trạng thái thị trường](http://internaltest.fpts.com.vn/EzLoans/Pages/ChayHeThong/Margin/MarketState.aspx) (MAMO.13)

> - Thuộc nghiệp vụ cuối ngày (sv endday)
> - Không gửi msg sang Account

b1: Gọi Sp cập nhật trạng thái thị trường

b2: Nếu đầu vào API MarketState=1 thì gọi thêm sp cập nhật danh sách các hợp đồng không được trả nợ


### [Tạo hợp đồng Margin](http://internaltest.fpts.com.vn/EzLoans/Pages/ChayHeThong/Margin/AddContract.aspx)

```
Tạo hợp đồng T+
b1: vào eztrade đặt lệnh mua Ký quỹ (TK phải đc đk T+)
b2: nhờ Loan khớp lệnh
b3: nhờ Thảo SST đẩy trade về nova
b4: vào form tạo hợp đồng marign bấm tổng hợp rồi tạo hđ


Thay đổi hạn mức trên eztrade/mobile
vào thay đổi, nếu phải duyệt thì vào hạn mức trên ezmargin để duyệt
nếu người duyệt có hạn mức nhỏ hơn hạn mức duyệt thì phải qua form duyệt quản lý rủi ro 

```


#### UC-14: Tổng hợp Trade mua Margin (để tạo HĐ Margin) (MAMO.14)

> - Thuộc nghiệp vụ cuối ngày (sv endday)
> - Không gửi msg sang topic Account
> - Command SumerizeMarginBuyCommand

- b1: Gọi API nova cung cấp danh sách trade mua margin **http://settle.trade.rs-dev.toms.fpts.com.vn:8086/api/v1/settle/TradeMarginGet?ptype=1** để lấy ra danh sách trade mua margin trong ngày
- b2: Gọi sp mamo **spmamo_mar_create_sum** để insert dữ liệu vào db
  - Exception gọi sp mamo fail thì api phản hồi false, code, msg lỗi

- API Tổng hợp Trade mua Margin (để tạo HĐ margin) **http://endday.mamo.sv-dev.loans.fpts.com.vn:8086/api/v1/Mamo/buy**


#### UC-14: Tìm kiếm DS HĐ margin cần tạo (MAMO.14)
> - Thuộc nghiệp vụ cuối ngày (api trong sv rs)

- API: **http://mamo.rs-dev.loans.fpts.com.vn:8086/api/v1/Margin/contracts/NAMNV**
- Gọi tới SP: **spmamo_mar_create_sum_get**


#### UC-14: Tạo HĐ Margin (MAMO.14)

> - Thuộc nghiệp vụ cuối ngày (sv endday)
> - Tăng dư nợ
> - Gửi msg Tiền sang topic Account
> - Xử lý trước, nhận phản hồi Account sau
> - Account không check số dư
> - Command CreateMarginCommand

- API Tạo hợp đồng Margin **http://endday.mamo.sv-dev.loans.fpts.com.vn:8086/api/v1/Mamo**
  
- b1: Check RequestId tại Log Input Memory
- b2: Gọi API Fee để lấy danh sách tài khoản đang dùng T+ **http://para.fee.rs-dev.toms.fpts.com.vn:8086/api/v1/fee/clientcode-T?type={type}** (gói T+ type=1; gói thường type=2)
- b3: Gọi SP **spmamo_mar_create_exec** làm nghiêp vụ tạo hợp đồng để xử lý và log input cho ALL row (lỗi 1 dòng thì update log input db và xử lý tiếp các dòng khác)
- b4: Gọi SP **spmamo_mar_create_exec** lấy danh sách **rs1** cần gửi msg sang topic Account (chỉ lấy các dòng đã xử lý thành công ở DB và chưa gửi Account)
  - Log input memory
  - Log sum memory
- b5: Gửi msg Tiền sang topic Account cho ALL row **Information.Account.Cash**
- b6: Nhận phải hồi Tiền từ topic Account **Information.Account.Cash.Output**
  - Check log input memory
  - Update log input memory
  - Update log sum memory
  - Check log sum: nếu đã nhận đủ phản hồi Account rồi thì:
    - Update log input db, log sum db
    - Gọi SP **spmamo_mar_create_exec_get** lấy danh sách dữ liệu để gửi msg ra topic Output Mamo
    - Gửi Pusher
  - Exception nhận phản hồi tiền Account Fail
    - Check log input memory
    - Update log input memory
    - Update log sum memory
    - Check log sum : nếu đã nhận đủ phản hồi Account rồi thì
      - Update log input db, log sum db
      - Gọi SP **spmamo_mar_create_exec_get** để lấy danh sách dữ liệu để gửi topic Output Mamo
      - Gửi Pusher

### PI Mamo
```
PI MAMO
  - b1: vào eztrade đặt lệnh bán HĐ Ký quỹ Margin (TK phải đc đk Margin có dùng T+ hoặc ko)
  - b2: nhờ Loan khớp lệnh
  - b3: nhờ Thảo SST đẩy trade về nova
  - b4: vào form PI bấm Tổng hợp rồi bấm PI
```
#### UC-16: Tổng hợp Trade bán Margin (để PI Margin) (MAMO.16)
> - Thuộc nghiệp vụ cuối ngày (sv endday)
> - Không gửi msg Account

- API tổng hợp PI **http://endday.mamo.sv-dev.loans.fpts.com.vn:8086/api/v1/Mamo/sell**
- b1: Gọi API nova **http://settle.trade.rs-dev.toms.fpts.com.vn:8086/api/v1/settle/TradeMarginGet?ptype=2** để lấy danh sách trade bán Margin trong ngày
  - Exception: nếu gọi api null -> return luôn
- b2: Gọi SP mamo **spmamo_pi_sum** để insert dữ liệu vào DB
  - Exception: SP không thành công thì phản hồi API là False, Code, Message lỗi

#### UC-16: Tạo GD trả nợ bằng bán ký quỹ PI (MAMO.16)
> - Thuộc nghiệp vụ cuối ngày (sv endday)
> - API xử lý cho N row
> - Giảm dư nợ
> - Gửi msg tiền sang Account
> - Xử lý trước, nhận phản hồi Account sau
> - Account không check số dư

- b1: Check RequestId (check tại Log Input Memory)
- b2: Gọi SP **mamo.spmamo_pi_exec** để làm nghiệp vụ xử lý và log input db cho all row (lỗi 1 dòng update log input và xử lý tiếp các dòng khác)
- b3: Lấy danh sách gửi Account (chỉ lấy các dòng đã xử lý thành công ở DB và chưa gửi Account)
- b4: Log Input Memory, Log Sum Memory
- b5: Gửi Msg Tiền sang topic cho Account **Information.Account.Cash**
- b6: Nhận phản hồi từ topic output Account **Information.Account.Cash.Output**
  - Check log input memory
  - Update log input memory
  - Update log sum memory
  - Check log sum: Nếu đã nhận đủ phản hồi Accout thì: Update log input db, log sum db
  - Exception: nhận phản hồi msg tiền Fail
    - Check log input memory
    - Update log input memory
    - Update log sum memory
- b7: Gửi Msg ra topic **Loans.Mamo.Output** Output Mamo (gọi sp **spmamo_pi_exec_get** để lấy danh sách dữ liệu)
- b8: gửi topic Pusher **Loans.Pusher**

#### UC-16: Tìm kiếm trade bán Margin (để PI Margin) 
> - Thuộc nghiệp vụ cuối ngày (sv endday)
> - API trả cứu/ tìm kiếm DS HĐ chưa PI **http://mamo.rs-dev.loans.fpts.com.vn:8086/api/v1/Margin/unpayment-institution**

- b1: Form PI Marmor bấm nút Tìm kiếm
- b2: Gọi tới API tra cứu/ tìm kiếm danh sách HĐ chưa PI
- b3: API gọi tới SP **spmamo_pi_get** để lấy ra danh sách


> - API Tìm kiếm Xóa hợp đồng thành lý **http://mamo.rs-dev.loans.fpts.com.vn:8086/api/v1/Margin/contracts/liquidated/deleted***
- b2: Gọi tới API Tìm kiếm Xóa hợp đồng thanh lý
- b3: API gọi tới API **http://ezopengtw-dev.customer.fpts.com.vn:8086/api/v1/Ezopen/fpts-insider-get** để lấy danh sách NNB, NLQ hiệu lực bên EzOpen
- b3: Lấy dữ liệu trả ra của API bên Open truyền vào SP **spmamo_autosell_delete_get** để hiển thị danh sách ra màn hình.

### Cập nhật hợp đồng Mamo (MAMO.19)
```
EzLoans/Pages/ChayHeThong/Margin/UpdateContract.aspx
```
- Bấm nút **Cập nhật** để gọi 2 api **UC-19**

#### UC-19: Cập nhật giá đóng cửa (để cập nhật hđ mamo khi chạy hệ thống) (MAMO.19)
> - Thuộc nghiệp vụ cuối ngày (sv endday)
> - API
> - Không cần gửi Account
> - Controler: Price
> - Service: Endday

API Cập nhật giá tham chiếu hoặc giá sàn. Nếu priceType=1 thì cập nhật giá tham chiếu, nếu là 3 thì cập nhật giá sàn **http://endday.mamo.sv-dev.loans.fpts.com.vn:8086/api/v1/Price**
- b1: Gọi API Price **http://dev.gateway.fpts.com.vn/news/api/Loans_Mamo/ClosePrice** để lấy giá đóng cửa của ALL các mã CK
  - Exception: API không có dữ liệu thì ghi log lỗi và return false
- b2: Gọi SP Mamo **spmamo_price_u** để insert DL vào DB
  - Exception: SP chạy không thành công thì phản hồi API là False, Code, Message lỗi

#### UC-19: Cập nhật HĐ mamo khi chạy HT (MAMO.19)
> - Thuộc nghiệp vụ Cuối ngày (sv endday)
> - Không gửi msg sang Account
> - API
> - Controler: Price
> - Service: Endday

API Cập nhật HĐ mamo khi chạy HT **http://endday.mamo.sv-uat.loans.fpts.com.vn:8086/api/v1/Price/contract**
- b1: Gọi SP **spmamo_contract_price_u** mamo để cập nhật HĐ
  - Exception: gọi SP thất bại thì phản hồi API là False, Code, Message lỗi
- b2: Lấy DL trả ra từ SP mamo: Loop để gọi SP RPT **rpt.spsms_insertsmsdata** gửi SMS
  - Exception: SP RPT lỗi thì ghi log, bỏ qua dòng đó để chạy dòng khác



### UC-20: Cập nhật giá sàn (khi tổng hợp các HĐ bị thanh lý và khi EOD) (MAMO.20)
> - Thuộc nghiệp vụ cuối ngày (sv endday)
> - API
> - Không gửi msg sang topic Account

- b1: Gọi API **http://trddev.toms-tradeorder.fpts.com.vn:8086/api/v1/stock/loans** của trd để lấy giá sàn của all các mã CK
  - Exception: API không có dữ liệu thì ghi log lỗi và return false
- b2: Gọi SP mamo **mamo.spmamo_price_u** để insert dữ liệu vào DB
  - Exception: SP mamo chạy không thành công thì phản hồi API là False, Code, Msg lỗi
  






### UC-21: Tổng hợp các HĐ bị thanh lý (MAMO.21)
> - Thuộc nghiệp vụ cuối ngày (sv endday)
> - Job chạy tự động lúc 17h01 hàng ngày
> - Không gửi msg sang topic Account

- b1: Đúng 17h01 hàng ngày từ thứ 2 đến thứ 6 Gọi SP validate **spmamo_auto_sell_validate** 
  - Exception: SP trả false thfi ghi log infor và return
- b2: Chạy cập nhật giá sàn (chạy UC-19: Cập nhật HĐ mamo khi chạy HT (MAMO.19))
  - Exception: Chạy cập nhật giá sàn lỗi thì ghi log lỗi và vẫn chạy tiếp các bước sau
- b3: Gọi SP nghiệp vụ **spmamo_auto_sell_sum** 
  - Exception: Chạy SP xử lý lỗi thì Gửi mail cho FIT

```
  API Tổng hợp các HĐ bị thanh lý **http://endday.mamo.sv-dev.loans.fpts.com.vn:8086/api/v1/Jobs/Summary-auto-sell**
```


### UC-22: Xóa HĐ mamo bị thanh lý (MAMO.22)



### UC-23: Settle trả nợ bằng bán ký quỹ (MAMO.23)
> - Thuộc nghiệp vụ cuối ngày (sv endday)
> - Job tự động chạy hàng ngày lúc 11h35 
> - Có API trong trường hợp cần chạy lại
> - Gửi msg Tiền sang topic Account (Account không xử lý, chỉ ghi log -> Ko cần nhận phản hồi Account)

API Settle trả nợ bẳng bán ký quỹ **http://endday.mamo.sv-dev.loans.fpts.com.vn:8086/api/v1/Jobs/settle-debit**
- b1: Gọi Sp **mamo.spmamo_sell_settle**
  - Exception: gọi SP Fail thì ghi lỗi
- b2: Lấy **rs** danh sách từ SP trả ra để gửi msg ra topic cho Account
- b3: Gửi msg Tiền sang topic Account **Information.Account.Cash** cho all row
- b4: Gửi msg Output Loans ra topic **Loans.Mamo.Output**



### UC-24: Cập nhật tham số Mamo cho từng TK (MAMO.24)



### CHẠY HỆ THỐNG
#### Form: Trạng thái thị trường mamo
b1: Ấn nút Cập nhật trên form để gọi tới API **http://endday.mamo.sv-dev.loans.fpts.com.vn:8086/api/v1/SystemLog**
b2: API gọi tới SP **spmamo_loging_i** để insert log 



### UC-25: Cập nhật tham số Mamo cho ALL KH (MAMO.25)
> - Thuộc nghiệp vụ cuối ngày (sv endday)

- b1: Gọi API **http://marparas-dev.para.fpts.com.vn:8086/api/Para/GetParameterEndDay** parameter mamo để lấy ALL DL gói, danh mục và gán gói
- b2: Gọi SP **mamo.spmamo_parameter_eod** để cập nhật DB


### UC-26: Cập nhật tham số phí HTV cho ALL KH (MAMO.26)
> - Thuộc nghiệp vụ cuối ngày (sv endday)
> - Job
> - Có API chạy thay Job

API Cập nhật tham số phí HTV cho ALL KH  **http://endday.mamo.sv-dev.loans.fpts.com.vn:8086/api/v1/Jobs/param/feerate**
- b1: Gọi API Fee **http://para.fee.rs-dev.toms.fpts.com.vn:8086/api/v1/fee/clientcode-T?type=2** để lấy DS tỉ lệ phí HTV của ALL TK (gói T+ thì type=1, gói thường type=2)
  - Exception: API Fee không có DL thì báo lỗi
- b2: Gọi SP **mamo.spmamo_htv_eod** để cập nhật DB


### UC-27: Đối chiếu PI (MAMO.27)
> - Thuộc nghiệp vụ cuối ngày (sv endday)
> - Viết API đối chiếu
> - Form: https://internaltest.fpts.com.vn/EzLoans/Pages/ChayHeThong/Margin/PI.aspx

- b1: user bấm nút Đối chiếu trên form Đối chiếu PI
- b2: Form gọi tới API **http://mamo.rs-dev.loans.fpts.com.vn:8086/api/v1/Comparison/PI**
- b3: API gọi SP Mamo **mamo.spmamo_compare_pi_get** để lấy danh sách PI ở Mamo
- b4: Gọi SP Nova **nova.spnova_doichieu_pi** để lấy danh sách PI ở Nova
- b5: Nếu cả Mamo và Nova đều không có dữ liệu thì **returncode=1; returnmessage="Đối chiếu thành công!; sumAmount=0, sumQuantityMar = 0, sumQuantityMor = 0**
- b6: Đối chiếu theo key là SettleId, ContractNUm, ClientCode, StockCode
  - GD PI có ở Mamo nhưng không có ở Nova
  - GD PI có ở Nova nhưng không có ở Mamo
  - Có ở cả Mamo và Nova nhưng lệch số (lệch một trong các giá trị Quantity, PayAmount)
- b7: Tính tổng: Lấy DS Mamo
  - SumAmount = tổng PayAmount ở Mamo
  - SumQuantityMar = tổng Quantity ở Mamo có TypeText='MAR'
  - SumQuantityMor = tổng Quantity ở Mamo có TypeText='MOR'
- b8: Nếu không có dòng nào lệch thì **returncode=1; returnmsg='Đối chiếu thành công!'; trả ra số tổng SumAmount, SumQuantityMar, SumQuantityMor**
- b9: Nếu có dòng lệch thì **returncode=2; returnmsg='Đối chiếu không thành công!'**


### UC-28: Đối chiếu hợp đồng Mamo (MAMO.28)
> - Thuộc nghiệp vụ Cuối ngày (sv api)
> - API đối chiếu HĐ Mamo
> - Form: https://internaltest.fpts.com.vn/EzLoans/Pages/ChayHeThong/Margin/DoiChieuHDKQ.aspx

- b1: User bấm Đối chiếu trên Form, sẽ gọi tới Api **http://mamo.rs-dev.loans.fpts.com.vn:8086/api/v1/Comparison/contract?agentGroup=ALL**
- b2: Api gọi SP Mamo **mamo.spmamo_compare_contract_get** để lấy danh sách HĐ ở Mamo
- b3: Gọi tiếp SP ở Nova để lấy danh sách HĐ ở Nova
- b4: Nếu cả Mamo và Nova đều không có dữ liệu thì **returncode=1; returnmsg='Đối chiếu thành công!; trả ra số tổng sumAmount=0; sumQuantity=0**
- b5: Đối chiếu theo key ContractNum
  - Nếu HĐ có ở Mamo nhưng không có ở Nova
  - Nếu HĐ có ở Nova nhưng không có ở Mamo
  - Nếu HĐ có ở cả Mamo và Nova nhưng lệch số (lệch một trong các giá trị startQuantity, startAmount)
- b6: Tính tổng -> lấy danh sách Mamo **SumAmount = tổng StartAmount ở Mamo; SumQuantity = tổng StartQuantity ở Mamo**
  - Nếu không có dòng nào lệch thì **returncode=1; returnmsg = 'Đối chiếu thành công!'; trả ra số tổng: SumAmount, SumQuantity'**
  - Nếu có dòng lệch thì **returncode=2; returnmsg='Đối chiếu không thành công!'; trả ra DS các dòng lệch gồm các cột: ContractNum, QuantityNova, AmountNova, QuantityMamo, AmountNova, Branch**

### UC-29: Đối chiếu trả nợ Mamo (MAMO.29)
> - Thuộc nghiệp vụ Cuối ngày (sv api)
> - API đối chiếu trả nợ mamo
> - Form: https://internaltest.fpts.com.vn/EzLoans/Pages/ChayHeThong/Margin/CompareDebtRepayment.aspx

- b1: User bấm Đối chiếu, form sẽ gọi tới API: **http://mamo.rs-dev.loans.fpts.com.vn:8086/api/v1/Comparison/debit?agentGroup=ALL**
- b2: API gọi SP Mamo để lấy danh sách trả nợ Mamo
- b3: Gọi tiếp SP ở Nova để lấy danh sách trả nợ ở Nova
- b4: Nếu cả Mamo và Nova đều không có dữ liệu thì **returncode=1; returnmsg='Đối chiếu thành công!'; trả ra số tổng: sumAmount=0; sumCharge=0**
- b5: Đối chiếu theo key là ContractNum
  - Nếu GD trả nợ có ở Mamo nhưng không có ở Nova
  - Nếu GD trả nợ có ở Nova nhưng không có ở Mamo
  - Nếu có ở cả Mamo và Nova nhưng lệch số (lệch 1 trong các giá trị PayAmount, Charge) thì b6
- b6: Tính tổng -> lấy DS Mamo **sumAmount = tổng PayAmount ở Mamo; sumCharge = tổng Charge ở Mamo**
  - Nếu không có dòng nào lệch thì **returncode=1; returnmsg = 'Đối chiếu thành công!'; trả ra số tổng sumAmount; sumCharge**
  - Nếu có dòng lệch thì **returncode=2; returnmsg='Đối chiếu không thành công!'; trả ra DS các dòng lệch gồm các cột ContractNum, ChargeNova, AmountNova, ChargeMamo, AmountMamo, Branche**


    
### UC-30: Thông báo cho KH các HĐ Mamo quá hạn (MAMO.30)
> - Thuộc nghiệp vụ Cuối ngày (sv endday)
> - Job
> - Chạy lúc 8h15 sáng, các ngày làm việc từ t2 đến t6

- API Thông báo cho các HĐ mamo bị quá hạn **http://endday.mamo.sv-dev.loans.fpts.com.vn:8086/api/v1/Jobs/notification/deadline-contract** 
- b1: Gọi SP **mamo.spmamo_contract_deadline** để insert dữ liệu vào bảng mail, rồi trả ra **rs** danh sách các HĐ quá hạn để gửi SMS
  - SP không có dữ liệu thì kết thúc Task
- b2: Gọi SP insert **rpt.spsms_insertsmsdata** để Gửi SMS cho KH các HĐ quá hạn


### UC-31: Thông báo trạng thái HĐ (tất toán/ rơi vào mức xử lý) Mamo (MAMO.31)

### UC-32: Thông báo cho KH sắp đến ngày GD KHQ
> - Thuộc nghiệp vụ cuối ngày (sv endday)
> - Job chạy lúc 20h từ thứ 2 đến thứ 6
> - Có API để chạy lại Job

- b1: Gọi API của CustId để lấy danh sách quyền sắp tới ngày GD KHQ
  - Exception: API không có dữ liệu thì không làm gì nữa, log infor
- b2: Gọi SP **spmamo_mail_gdkhq** xử lý để insert bảng mail 

### UC-36: Cập nhật Broker ưu tiên của KH (MAMO.36)
> - Thuộc nghiệp vụ cuối ngày (sv endday)

API Cập nhật DS broker được gán cho KH **http://endday.mamo.sv-dev.loans.fpts.com.vn:8086/api/v1/Mamo/broker**
- b1: Gọi API **http://para.fee.rs-dev.toms.fpts.com.vn:8086/api/v1/fee/broker-actvice-mamo** của Fee để lấy DS cần cập nhật (lấy all dữ liệu)
  - Exception: API không có dữ liệu thì báo lỗi
- b2: Gọi SP **mamo.spmamo_brokercust_i** để cập nhật DS vào DB: truyền p_Action = 2, p_list_brokercust = DS từ API


### UC-37: Chốt DL cuối ngày - EOD Mamo (MAMO.37)
> - Thuộc nghiệp vụ cuối ngày (sv endday)
> - Job Service
> - Thời gian chạy: Sau khi active phí cuối  ngày done, sau khi EOD TRD done (active tham số mamo cuối ngày done)

- b1: Consume Msg Topic Fee: **Fee.Trade.Flags** (check có msg active phí cuối ngày xong: EodFee=1
{
  "EodFee": 1,
  "Alastupdate": "2024-07-29T18:22:15.8444381+07:00"
}
- b2: Gọi SP **trd.sptrd_check_eod_bod** TRD check EOD TRD done
- b3: Cập nhật broker ưu tiên của KH (chạy UC-36)
- b4: Cập nhật tham số phí HTV cho ALL KH (chạy UC-26)
- b5: Cập nhật tham số cho ALL KH (chạy UC-25)
- b6: Cập nhật giá sàn (chạy UC-20)
- b7: Gọi SP **mamo.spmamo_sum** chốt DL Mamo
- Exception:
  - Check TRD chưa EOD thì đợi 1 phút sau check lại
  - Lỗi 1 bước thì dừng lại và mail thông báo lỗi



### UC: Tra cứu tham số - HĐ ký quỹ trên EzTrade
> - Thuộc sv api (LoansMamo.Api)
> - Api tra cứu **http://mamo.rs-uat.loans.fpts.com.vn:8086/api/v1/Margin/contracts**
> - Api gọi tới SP Mamo tra cứu **spmamo_searchcontract_eztrade**




### Fix lỗi
#### Lỗi Cầm cố CK đang về không hiện lên để cầm cố CK
- Check Mã CK được khớp lệnh mua theo lệnh thường không? (nếu mua lệnh Margin thì sẽ không lên)
- Check Mã CK được được khớp có nằm trong danh mục vay ký quỹ hay không? (nếu không nằm trong danh mục vay ký quỹ thì sẽ không cầm cố được)
- Check thời gian đẩy nova của mã CK là khi nào (nếu sau 15h45 và trước 12h15 thì sẽ chưa hiển thị ck đang về được vì chưa tới giờ chạy job)

  
 
    









