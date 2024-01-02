#import <CoreData/CoreData.h>

@interface CoreDataSingleton : NSObject

@property (readonly, strong) NSPersistentContainer *persistentContainer;

+ (instancetype)sharedInstance;
- (void)saveContext;
- (NSManagedObject *)insertEntityWithName:(NSString *)entityName;
- (NSArray *)fetchEntitiesWithName:(NSString *)entityName predicate:(NSPredicate *)predicate sortDescriptors:(NSArray<NSSortDescriptor *> *)sortDescriptors;
- (void)updateEntity:(NSManagedObject *)entity;
- (void)deleteEntity:(NSManagedObject *)entity;

@end



#import "CoreDataSingleton.h"

@implementation CoreDataSingleton

+ (instancetype)sharedInstance {
    static CoreDataSingleton *sharedInstance = nil;
    static dispatch_once_t onceToken;
    dispatch_once(&onceToken, ^{
        sharedInstance = [[self alloc] init];
    });
    return sharedInstance;
}

- (NSPersistentContainer *)persistentContainer {
    @synchronized (self) {
        if (!_persistentContainer) {
            _persistentContainer = [[NSPersistentContainer alloc] initWithName:@"YourDataModelName"];
            [_persistentContainer loadPersistentStoresWithCompletionHandler:^(NSPersistentStoreDescription *storeDescription, NSError *error) {
                if (error) {
                    NSLog(@"Unresolved error %@, %@", error, error.userInfo);
                    abort();
                }
            }];
        }
    }
    return _persistentContainer;
}

- (void)saveContext {
    NSManagedObjectContext *context = self.persistentContainer.viewContext;
    NSError *error = nil;
    if ([context hasChanges] && ![context save:&error]) {
        NSLog(@"Unresolved error %@, %@", error, error.userInfo);
        abort();
    }
}

- (NSManagedObject *)insertEntityWithName:(NSString *)entityName {
    NSManagedObjectContext *context = self.persistentContainer.newBackgroundContext;
    NSManagedObject *newEntity = [NSEntityDescription insertNewObjectForEntityForName:entityName inManagedObjectContext:context];
    return newEntity;
}

- (NSArray *)fetchEntitiesWithName:(NSString *)entityName predicate:(NSPredicate *)predicate sortDescriptors:(NSArray<NSSortDescriptor *> *)sortDescriptors {
    NSManagedObjectContext *context = self.persistentContainer.viewContext;
    NSFetchRequest *fetchRequest = [NSFetchRequest fetchRequestWithEntityName:entityName];
    fetchRequest.predicate = predicate;
    fetchRequest.sortDescriptors = sortDescriptors;
    NSError *error = nil;
    NSArray *result = [context executeFetchRequest:fetchRequest error:&error];
    if (error) {
        NSLog(@"Fetch error %@, %@", error, error.userInfo);
    }
    return result;
}

- (void)updateEntity:(NSManagedObject *)entity {
    NSManagedObjectContext *context = entity.managedObjectContext;
    NSError *error = nil;
    if (![context save:&error]) {
        NSLog(@"Update error %@, %@", error, error.userInfo);
    }
}

- (void)deleteEntity:(NSManagedObject *)entity {
    NSManagedObjectContext *context = entity.managedObjectContext;
    [context deleteObject:entity];
    [self saveContext];
}

@end