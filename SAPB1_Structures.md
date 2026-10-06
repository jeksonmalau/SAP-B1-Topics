### 📊 SAP B1 Core Tables 
The diagram below illustrates the Entity Relationship Diagram (ERD) of the source SAP B1 tables
```mermaid
erDiagram
    %% --- Lapisan sumbe: Data Master SAP B1
    OCRD_Customer_Master {
        string CardCode PK "Kode Pelanggan"
        string CardName "Nama Pelanggan"
        string GroupCode "Group Department"
    }
    OITM_Item_Master{
        string ItemCode PK "Kode Barang"
        string ItemName "Nama Barang"
        string ItmsGrpCode "Kategori Produk"                                             
    }
    OINV_Invoice_Header{
        int DocEntry PK "ID Internal"
        int DocNum "Nomor Document"
        date DocDate "Tanggal Transaksi"
        string CardCode "Kode Pelanggan"
        double DocTotal "Total Penjualan"
    }
    INV1_Invoice_Rows{
        int DocEntry PK, FK "ID Internal"
        int LineNum PK "Nomor Baris"
        string ItemCode FK "Kode Barang"
        double Price "Harga Satuan"
        double Quantity "Jumlah Barang"
        double LineTotal "Total perbaris"
    }
    %% --- Hubungkan antar table --- %%
    OINV_Invoice_Header ||--|{ INV1_Invoice_Rows : "plance"
    OCRD_Customer_Master ||--o{ OINV_Invoice_Header : "contains"
    OITM_Item_Master ||--o{ INV1_Invoice_Rows : "order_in"