 NSMutableSet *uniqueTimestamps = [NSMutableSet set];
    
    for (NSString *dataString in dataArray) {
        NSString * newString = [dataString stringByDeletingPathExtension];
        [uniqueTimestamps addObject:newString];
        
    }
    
    NSPredicate *predicate = [NSPredicate predicateWithFormat:@"SELF CONTAINS 'bb-' AND NOT SELF CONTAINS 'json'"];
    
    // 将结果转换为数组
    NSArray *resultArray = [uniqueTimestamps allObjects];
    NSLog(@"%@", resultArray);


find /Users/lucas/Desktop/111/ -type f -name 'log-bb-12-13-14*' ! -name '*.json' -exec mv {} /Users/lucas/Desktop/111/b/ \;
