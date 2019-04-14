#include <string>
#include <iostream>
#include <cstdio>
#include <vector>
using namespace std;
int r=256;   //liczba symboli alfabetu
int q=9551;  //mo¿liwie du¿a liczba pierwsza

vector <int> naive( const string& str, const string& text )
{
    vector <int> pos;
    int dl_t = text.length(), dl_w = str.length();
    bool ok = 0;

    for( int i=0; i <= dl_t - dl_w; i++ )
    {
        ok = 1;

        for( int j=0; j < dl_w; j++ )
        {   if( text[j+i] != str[j] )
            {
                ok = 0;
                break;
            }
        }
        if( ok )
        {
            pos.push_back( i );
        }
    }

    return pos;
}

vector <int> prefix( const string& str )
{
    vector <int> P;
    P.push_back(0);
    P.push_back(0);
    int t=0;
    for( int j = 2; j <= str.length(); j++)
    {
        while( ( t > 0 ) && ( str[ t ] != str[ j-1 ]) ) t = P[ t ];
        if( str[ t ] == str[ j-1 ] ) t++;
        P.push_back( t );
    }
    return P;
}

vector <int> KMP( const string& str, const string& text )
{
    int i=1;
    int j=0;
    int n = text.length();
    int m = str.length();
    vector <int> P;
    vector <int> pos;
    P = prefix( str );

    /*for( int x = 1; x < P.size(); x++ )
    {
        cout << P[ x ] << ' ';
    }*/
    while( i <= n-m+1 )
    {
        j = P[ j ];
        while( ( j < m ) && ( str[ j ] == text[ i+j-1 ] ) )
        {
            j++;
        }
        if( j == m ){ pos.push_back( i );  }
        i = i + max( 1, j-P[ j ] );
    }
    return pos;
}

int power_modulo_fast(int a, int b, int m)
{
    int i;
    int result = 1;
    long int x = a%m;

    for( i = 1; i <= b; i <<=1 )
    {
        x %= m;
        if( ( b&i ) != 0 )
        {
        result *= x;
        result %= m;
        }
        x *= x;
    }
    return result%m;
}

int h(string str) //algorytm Hornera
{
    int m = str.length();
    int hx = 0;
    for( int i = 0; i < m; i++ )
    {
        hx = ( ( hx*r ) + str[ i ] );
        hx %= q;
    }
    return hx;
}

vector <int> RK( const string& str, const string& text )
{
    vector <int> pos;
    int h1 = h( str );
    int h2 = h( text );

    int rm;
    int n = text.length();
    int m = str.length();

    rm = power_modulo_fast(r, m-1, q);
    int j, i = 0;

    while ( i < n-m )
    {
        j = 0;
        //cout<< h1 << " "<<h2<<endl;
        if( h1 == h2 ) while( ( j < m ) && ( str[ j ] == text[ i+j ] ) ) j++;

        if( j == m) pos.push_back( i+1 );
        h2 = ( ( h2-text[ i ]*rm )*r+text[ i+m ] );
        h2 %= q;
        if( h2 < 0 ) h2+=q;
        i++;
    }

    return pos;
}

int main()
{
    vector <int> pos;
    pos = RK("ma", "mamamamam");

    for( int i = 0; i < pos.size(); i++ )
    {
        cout << pos[ i ] << " ";
    }
    /*
    vector <int> p;
    p=prefix("bbbabb");
    for( int i = 1; i < p.size(); i++ )
    {
        cout << p[ i ] << ' ';
    }*/
    return 0;
}
