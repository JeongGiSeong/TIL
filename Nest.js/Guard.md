## CanActivate

CanActivate는 NestJS의 가드(Guard) 인터페이스  
가드는 특정 경로에 대한 요청을 처리하기 전에 실행되어, 요청이 허용될지 여부를 결정  
CanActivate 인터페이스는 canActivate 메서드를 구현하도록 요구하며, 이 메서드는 boolean 값을 반환하여 요청을 허용할지(true) 거부할지(false) 결정합니다.

```typescript
import { Injectable, CanActivate, ExecutionContext } from '@nestjs/common';

@Injectable()
export class AuthGuard implements CanActivate {
  canActivate(context: ExecutionContext): boolean {
    const request = context.switchToHttp().getRequest();
    return validateRequest(request);
  }
}
```
