---  
Keywords: auditd, awk, CentOS, RHEL  
Copyright: (C) 2021 Toshiya Kiyokawa  
---  
# 監査ログ(audit.log)で同一ログを1行で表示する

## これは何？
auditdの監査ログは、複数行で記録される。  
お勉強として同一ログを一行で表示するAWKを書いてみた。  
※十分にテストしていないから、バグあるかも。  
## Howto
    cat /var/log/audit/audit.log  | awk '
    # Change Key and Display DATE
    {
      if( KEY=="" || !match( $0, KEY) ) {
        # Set KEY: KEY=epoc time + ID (XXXXXX.XXX:ID)
        match($0,/\(.*\)/)
        KEY=substr($0, RSTART+1, RLENGTH-2)
        
        # Set ID
        split(KEY, tmp, ":")
        ID=tmp[2]
        
        # Set DATE
        match(KEY,/[0-9]+/)
        DATE=strftime("%Y/%m/%D %H:%M:%S" ,substr(KEY, RSTART, RLENGTH) )
        
        # Display DATE ID
        printf("\n%s %s",DATE,ID)
      }
      # Display Record Then same Time:ID
      if(match( $0,KEY )){ printf(" %s",$0) }
    }
    END{ printf("\n") }
    '
  
