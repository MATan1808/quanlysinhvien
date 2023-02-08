# quanlysinhvien
#include <bits/stdc++.h>
#include "filecuatoi.h"
#include <conio.h>
int getch();
using namespace std;
struct sv {
	int msv;
	string name;
	string lop;
	string brith;
	float gba;
	void in() {
		cout<<" Nhap MSV :";
		cin>>msv;
		cout<<" Nhap ten SV :";
		cin.ignore();
		getline(cin,name);
		cout<<" Nhap Ngay Sinh :";
		getline(cin,brith);
		cout<<" Nhap GBA :";
		cin>>gba;
		doimau(10);
		Sleep(1000);
		cout<<" \n nhap lua chon tiep theo  "<<endl;
	}
	void out() {
		cout<<setw(40)<<"\n-------------------------------------------------------------------------------\n";
		cout<<setw(40)<<" MSV :"<<msv<<" "<<endl;
		cout<<setw(40)<<" Ten SV :"<<name<<" "<<endl;
		cout<<setw(40)<<" Ngay Sinh :"<<brith<<" "<<endl;
		cout<<setw(40)<<" GBA :"<<gba<<" "<<endl;
		cout<<setw(40)<<"\n------------------------------------------------------------------------------\n"; 
 
	}
};
void nhap(int n, sv a[]) {
	for (int i=0; i<n; i++) {
		a[i].in();
	}
}
 
void xuat(int n, sv a[]) {
	for (int i=0; i<n; i++) {
		cout<<setw(30)<<"thong tin sinh vien "<<i+1<<endl;
		doimau(i+1);
		a[i].out();
	}	
}
 
void findd(int n, sv a[]) {
	int q;
	doimau(2);
	cout<<"nhap  can tim ";
	cin>>q;
	for (int i=0; i<n; i++) {
	if (a[i].msv == q) {
		a[i].out();
		}
	}
}
 
void timkiem(int n, sv a[]) {
	string ten;\
	doimau(1);
	cout<<"nhap ten sinh vien can tim :";
	cin.ignore();
	getline(cin,ten);
	bool check=0;
	for (int i=0; i<n; i++) {
		if (a[i].name.find(ten) != string::npos) {
			doimau(3);
			a[i].out();
			check=1;
		}
 
		if (!check) {
			doimau(6);
			cout<<"khong tim thay ";
			break;
		}
	}
}
 
void maxgba (int n, sv a[]) {
	int max=0;
	doimau(4);
	cout<<"thong tin sinh vien co GBA cao nhat la :"<<endl;
	for (int i=0; i<n; i++) {
		if (a[i].gba > max ){
			max=a[i].gba;
		}
	}
	for (int i=0; i<n; i++) {
		if (max==a[i].gba) {
			a[i].out();
		}
	}
} 

void mingba (int n, sv a[]) {
	int min=0;
	for (int i=0; i<n; i++) {
		if (a[i].gba < 2 ){
			min=a[i].gba;
		}
	}
	cout<<"sinh vien co GBA <= 2.5 \n";
	for (int i=0; i<n; i++) {
		if (a[i].gba == min) {
			a[i].out();
		}
		else {
			doimau(4);
			cout<<" khong tim thay !!!\n ";
			break;
		}
	}
}
// xuat ra theo thu tu diem gba tang dan 
bool cmd (sv a, sv b) {
	return a.gba > b.gba;
}
// tim kiem gba >=2.5 theo vector
void findgba (int n, sv a[]) {
	vector<sv> V;
	int c=0;
	for (int i=0; i<n; i++) {
		if (a[i].gba >= 2.5 ){
			V.push_back(a[i]);
			c++;
		}
	}
	sort (V.begin(), V.end(), cmd);
	cout<<"danh sach cac hoc sinh diem co gba tren  2.5 \n";
	for ( sv x: V) {
		x.in(); 
	}
	if (c == 0) cout<<"khong co ai co GBA >=2.5 \n";
}


void findgba1 (int n, sv a[]) {
	int min=0;
	for (int i=0; i<n; i++) {
		if (a[i].gba >= 2.5 ){
			min=a[i].gba;
		}
	}
	doimau(12);
	cout<<"sinh vien co GBA .= 2.5 \n";
	for (int i=0; i<n; i++) {
		if (a[i].gba == min) {
			a[i].out();
		}
		else {
			doimau(4);
			cout<<" khong tim thay !!!\n ";
			break;
		}
	}
}
// tach tu 
/*
vd Nguyen Van A
nguyen 
van 
a

*/
 vector<string>chuanhoa(string name) {
	stringstream ss(name);
	string token;
	vector<string> v;
	while (ss >> token){
		v.push_back(token);
	}
	return v;
}
// sap xep theo ten 
bool cmp2 (sv a, sv b) {
	vector<string> v1,v2;
	v1=chuanhoa(a.name);
	v2=chuanhoa(b.name);
	if (v1.back() != v2.back()) return v1.back() < v2.back();
	int len1 = v1.size();
	int len2 = v2.size();
	for (int i=0; i>min(len1,len2); i++) {
		if (v1[i] != v2[i]) return v1[i] < v2[i];
	}	
	return len1 < len2;
}
void sapxepten (int n, sv a[]) {
	for (int i=0; i<n; i++) {
		sort (a, a + n, cmp2 );
	}
}
bool cmp3 (sv a, sv b) {
	if (a.lop != b.lop) return a.lop < b.lop;
	vector<string> v1,v2;
	v1=chuanhoa(a.name);
	v2=chuanhoa(b.name);
	if (v1.back() != v2.back()) return v1.back() < v2.back();
	int len1 = v1.size();
	int len2 = v2.size();
	for (int i=0; i>min(len1,len2); i++) {
		if (v1[i] != v2[i]) return v1[i] < v2[i];
	}	
	return len1 < len2;	
}

bool cmp4 (sv a, sv b) {
	if (a.lop != b.lop) return a.lop < b.lop;
	return a.gba < b.gba;
	
}
void sapxeplop(int n, sv a[]) {
	sort(a, a+n, cmp3);
}
void sapxepgba(int n, sv a[]) {
	sort(a, a+n, cmp4);
}
int n=0;
sv a[1000];

int main () {
	doimau(6);
	cout<<setw(150)<<"MA Nguyen Nhat Tan  "<<endl;
//	int n=0;
//	cout<<"nhap so luong sinh vien \n";
//	cin>>n;
//	sv a[10000];
	//nhap(n,a);
	while (1) {
		doimau(3);
		cout<<"\n________________________MENU_____________________________________\n"; 
		cout<<"|1: 	nhap sinh vien                                          |\n";
		cout<<"|2: 	xuat toan bo sinh vien                                  |\n";
		cout<<"|3: 	tim kiem sinh vien                                      |\n";
		cout<<"|4: 	tim kiem sinh vien co diem GBA cao nhat                 |\n";
		cout<<"|5: 	liet ke sinh vien do diem GBA duoi 2,5                  |\n";
		cout<<"|6: 	liet ke sinh vien do diem GBA co va lon hon  2,5        |\n";
		cout<<"|7: 	test mau                                                |\n";
		cout<<"|8: 	sap xep theo ten                                        |\n";
		cout<<"|9: 	sap xep theo lop                                        |\n";
		cout<<"|10: sap xep theo lop voi gba giam dan                    	|\n";
		cout<<"|0: 	THOAT TRUONG TRINH !!!!!                                |\n";
		cout<<"|_____________________KET_THUC__________________________________|\n"; 
		int lc;
		doimau(2);
		cout<<" \nmoi nhap lua chon ! \n";
		cin>>lc; 
		if (lc == 1) {
			xoamanhinh();
			doimau(1);
			a[n].in();
			++n;			
		}
		else if (lc == 2) {
			xoamanhinh();
			doimau(3);
			xuat(n,a);
			cout<<endl;
			if (n == 0) {
				cout<<"ban chua nhap thong tin nao \n";
				cout<<"xin nhap thong tin \n";
				Sleep(2000);
				doimau(2);
				cout<<"\n\n\n\nnhan Enter de tiep tuc........\n";
			}
			system("Pause");
		} 
		else if (lc == 3) {
			doimau(4);
			if (n == 0) {
				cout<<"ban chua nhap thong tin nao \n";
				cout<<"xin nhap thong tin \n";
				Sleep(2000);
				doimau(2);
				cout<<"\n\n\n\nnhan Enter de tiep tuc........\n";
			}
			else 			
			timkiem(n,a);
			
		}
		else if (lc == 4) {
			doimau(5);
			if (n == 0) {
				cout<<"ban chua nhap thong tin nao \n";
				cout<<"xin nhap thong tin \n";
				Sleep(2000);
				doimau(2);
				cout<<"\n\n\n\nnhan Enter de tiep tuc........\n";
			}			
			 else maxgba(n,a);
		}
		else if (lc == 5) {
			doimau(6);
			if (n == 0) {
				cout<<"ban chua nhap thong tin nao \n";
				cout<<"xin nhap thong tin \n";
				Sleep(2000);
				doimau(2);
				cout<<"\n\n\n\nnhan Enter de tiep tuc........\n";
			}			
			 else mingba(n,a);
		//	findgba(n,a);
		}
		else if (lc == 6) {
			doimau(7);
			if (n == 0) {
				cout<<"ban chua nhap thong tin nao \n";
				cout<<"xin nhap thong tin \n";
				Sleep(2000);
				doimau(2);
				cout<<"\n\n\n\nnhan Enter de tiep tuc........\n";
			}			
			else findgba1(n,a);
		}
		else if (lc ==7) {
			cout<<"test mau \n";
			int n; 
			cin>>n;
			testmau(n);
			cout<<endl;
		}
		else if (lc == 8) {
			doimau(3);
			if (n == 0) {
				cout<<"ban chua nhap thong tin nao \n";
				cout<<"xin nhap thong tin \n";
				Sleep(2000);
				doimau(2);
				cout<<"\n\n\n\nnhan Enter de tiep tuc........\n";
			}
			else {
			cout<<"da sap xep \n";
			sapxepten(n,a);
		}
		}
		else if (lc == 9) {
			doimau(8);
			if (n == 0) {
				cout<<"ban chua nhap thong tin nao \n";
				cout<<"xin nhap thong tin \n";
				Sleep(2000);
				doimau(2);
				cout<<"\n\n\n\nnhan Enter de tiep tuc........\n";
			}			
			sapxepten(n,a);
			doimau(3);
			cout<<"da sap xep \n";
		}
		else if (lc == 10) {
			doimau(9);
			if (n == 0) {
				cout<<"ban chua nhap thong tin nao \n";
				cout<<"xin nhap thong tin \n";
				Sleep(2000);
				doimau(2);
				cout<<"\n\n\n\nnhan Enter de tiep tuc........\n";
			}			
			sapxeplop(n,a);
			doimau(3);
			cout<<"da sap xep \n";
		}
		else if (lc == 11) {
			doimau(10);
			if (n == 0) {
				cout<<"ban chua nhap thong tin nao \n";
				cout<<"xin nhap thong tin \n";
				Sleep(2000);
				doimau(2);
				cout<<"\n\n\n\nnhan Enter de tiep tuc........\n";
			}			
			sapxepgba(n,a);
			doimau(3);
			cout<<"da sap xep \n";
		}
		else if (lc ==0) {
			xoamanhinh();
			doimau(6);
			cout<<setw(100)<<" \n\n\n\n\n\t\t\t\t\t KET THUC !!!! \n";
			cout<<"\n-------------------------------------------------------\n";
			//xoamanhinh();
			system("pause");
			break;
		}
	}
 
 
}
