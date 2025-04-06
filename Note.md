# Regfile
1. `biriscv_regfile.sv` & `biriscv_xilinx_2r1w.sv`
2. biriscv_regfile分三種構成regfile的模式
>   1.  Xilinx FPGA 中的內建資源（如 Block RAM 或專用硬體構造） 來實作暫存器檔 (SUPPORT_REGFILE_XILINX && SUPPORT_DUAL_ISSUE)
>    >   ![1743921206472-screenshot](https://github.com/user-attachments/assets/fb73773f-500e-4355-83d8-b9ae850ab11d)
>    > - 用4個`biriscv_xilinx_2r1w`兜成
>    > - Path 0的rd(i.e. rd0)寫u_a_0, u_b_0, Path 1的寫u_a_1, u_b_1
>    > - 讀取rs時依照
>    >   > 1. 最近一次寫入的來源(rd0 or rd1)
>    >   > 2. 要output到path1還是path2
>    > 來判斷該從哪個2r1w reg取得rs
>   2.  直接用4r2w regfile (else)
>   3.  Single issue mode, 還是用Xilinx FPGA 中的內建資源 (SUPPORT_REGFILE_XILINX && !SUPPORT_DUAL_ISSUE)
