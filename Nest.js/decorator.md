## 데코레이터 (Decorators)

- [데코레이터 (Decorators)](#데코레이터-decorators)
  - [개요](#개요)
  - [데코레이터의 종류](#데코레이터의-종류)
    - [클래스 데코레이터](#클래스-데코레이터)
    - [메서드 데코레이터](#메서드-데코레이터)
    - [속성 데코레이터](#속성-데코레이터)
    - [매개변수 데코레이터](#매개변수-데코레이터)
    - [커스텀 데코레이터](#커스텀-데코레이터)

### 개요

데코레이터는 클래스, 메서드, 속성 또는 매개변수에 추가적인 메타데이터를 부여하여 특정 동작을 정의하거나 수정할 수 있게 하는 기능입니다.  
NestJS에서 데코레이터는 스프링의 어노테이션과 유사한 역할을 합니다.

<br>

### 데코레이터의 종류

#### 클래스 데코레이터

```TypeScript
@Controller('users')
export class UserController {}
```

#### 메서드 데코레이터

```TypeScript
@Get()
findAll() {
  return this.userService.findAll();
}
```

#### 속성 데코레이터

```TypeScript
@Prop()
name: string;
```

#### 매개변수 데코레이터

```TypeScript
@Param('id') id: string
```

#### 커스텀 데코레이터

```TypeScript
import { SetMetadata } from '@nestjs/common';
import { Role } from '../enums/role.enum';

export const ROLE_KEY = 'roles';
export const Roles = (...roles: Role[]) => SetMetadata(ROLE_KEY, roles);
```

```TypeScript
@Controller('admin')
export class AdminController {
  @Roles(Role.Admin)
  @Get()
  getAdminData() {
    // 관리자만 접근 가능한 로직
  }
}
```
