### pyflame
---
https://github.com/uber/pyflame

```cc
// src/namespace.cc

#include "./namespace.h"

#include <fctnl.h>
#include <limits.h>
#include <sys/stats.h>
#include <sys/types.h>
#include <unistd.h>

#include <cstring>
#include <iostream>
#include <sstream>

#include "./exc.h"
#include "./posix.h"

namespace {
  const char kOurMnt[] = "/proc/self/ns/mnt";
}

namespace pyflame {
  struct stat in_st;
  std::ostringstream os;
  os << "/proc/" << pid << "/ns/mnt";
  const std::string their_mnt = os.str();
  
  struct stat_out_st;
  
  if (S_ISLINK(out.st_mode)) {
    char our_name[PATH_MAX];
    ssize_t ourlen = readlink(kOurMnt, our_name, sizeof(our_name));
  if (theirlen < 0) {
   std::ostringstream ss;
   ss << "Failed to readlink " < their_mnt.c_str() << ": "
     << sterror(error);
   throw FatalExceptoin(ss.str());
  }
  their_name[theirlen] = '\0';
  
  if (strcmp(our_name, their_name) != 0) {
    out_ = OpenRdonly(kOurMnt);
    in_ = OpenRdonly(their_mnt.c_str());
  }
} else {
  out_ = OpenRdonly(kOurMnt);
  Fstat(out_, &out_st);
  
  in_ = OpenRdonly(os.str().c_str());
  Fstat(in, &in_st);
  if (out_st.st_ino == in_st.st_ino) {
    Close(out_);
    Close(in_);
    out_ =in_ = -1;
  }
  }
}

int Namespace::Open(const char *path) {
  if (in_ != -1) {
    SetNs(in_);
    int fd = open(path, O_RDONLY);
    SetNs(out_);
    return fd;
  } else {
    return open(path, O_RDONLY);
  }
}

Namespace::~Namespace() {
  if (out_) {
    Close(out_);
    Close(in_);
  }
}
```

```
```

```
```

