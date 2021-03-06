AM_CPPFLAGS = -DLOCALEDIR=\"$(localedir)\" -D_FILE_OFFSET_BITS=64
LDADD = $(LIBINTL)
sbin_PROGRAMS=partclone.info partclone.dd partclone.restore partclone.chkimg partclone.imager
TOOLBOX = srcdir=$(top_srcdir) builddir=$(top_builddir) $(top_srcdir)/toolbox

BTRFS_SOURCE= btrfs/crc32c.c btrfs/disk-io.c btrfs/extent-tree.c btrfs/inode-map.c btrfs/rbtree.c btrfs/volumes.c btrfs/ctree.c btrfs/extent-cache.c btrfs/file-item.c btrfs/print-tree.c btrfs/root-tree.c btrfs/dir-item.c btrfs/extent_io.c btrfs/inode-item.c btrfs/radix-tree.c btrfs/utils.c btrfs/crc32c.h btrfs/extent-cache.h btrfs/ioctl.h btrfs/print-tree.h btrfs/transaction.h btrfs/volumes.h btrfs/ctree.h btrfs/extent_io.h btrfs/kerncompat.h btrfs/radix-tree.h btrfs/utils.h btrfs/disk-io.h btrfs/hash.h btrfs/list.h btrfs/rbtree.h btrfs/version.h btrfs/repair.h btrfs/repair.c btrfs/raid6.c
#BTRFS_SOURCE= btrfs/*
EXFATFS_SOURCE= exfat/byteorder.h exfat/cluster.c exfat/exfatfs.h exfat/exfat.h exfat/io.c exfat/libexfat.a exfat/log.c exfat/lookup.c exfat/mount.c exfat/node.c exfat/time.c exfat/utf.c exfat/utils.c exfat/version.h

if ENABLE_STATIC
AM_LDFLAGS=-static
endif

if ENABLE_TINFO
LIBS+=-ltinfo
endif

AM_CFLAGS=-D_FILE_OFFSET_BITS=64

if ENABLE_MEMTRACE
AM_CFLAGS+=-DMEMTRACE -DMEMWATCH -DMW_STDIO
endif

if ENABLE_NCURSESW
AM_CFLAGS+=-I/usr/include/ncursesw
endif

version.h: FORCE
	$(TOOLBOX) --update-version

main_files=main.c partclone.c progress.c checksum.c partclone.h progress.h gettext.h checksum.h

partclone_info_SOURCES=info.c partclone.c checksum.c partclone.h fs_common.h checksum.h

partclone_restore_SOURCES=$(main_files) ddclone.c ddclone.h
partclone_restore_CFLAGS=-DRESTORE -DDD

partclone_chkimg_SOURCES=$(main_files) ddclone.c ddclone.h
partclone_chkimg_CFLAGS=-DCHKIMG -DDD

partclone_dd_SOURCES=$(main_files) ddclone.c ddclone.h
partclone_dd_CFLAGS=-DDD

partclone_imager_SOURCES=$(main_files) ddclone.c ddclone.h
partclone_imager_CFLAGS=-DIMG

if ENABLE_EXTFS
sbin_PROGRAMS += partclone.extfs
partclone_extfs_SOURCES=$(main_files) extfsclone.c extfsclone.h
partclone_extfs_CFLAGS=-DEXTFS
partclone_extfs_LDADD=-lext2fs -lcom_err -lpthread
endif

if ENABLE_REISERFS
sbin_PROGRAMS += partclone.reiserfs
partclone_reiserfs_SOURCES=$(main_files) reiserfsclone.c reiserfsclone.h
partclone_reiserfs_CFLAGS=-DREISERFS
partclone_reiserfs_LDADD=-lreiserfs -ldal
endif

if ENABLE_REISER4
sbin_PROGRAMS += partclone.reiser4
partclone_reiser4_SOURCES=$(main_files) reiser4clone.c reiser4clone.h
partclone_reiser4_CFLAGS=-DREISER4
partclone_reiser4_LDADD=-lreiser4 -laal
endif

if ENABLE_HFSP
sbin_PROGRAMS += partclone.hfsp
partclone_hfsp_SOURCES=$(main_files) hfsplusclone.c hfsplusclone.h
partclone_hfsp_CFLAGS=-DHFSPLUS
endif

if ENABLE_XFS
sbin_PROGRAMS += partclone.xfs
partclone_xfs_SOURCES=$(main_files) xfsclone.c xfsclone.h
partclone_xfs_CFLAGS=-DXFS
partclone_xfs_LDADD=-lxfs -lrt -lpthread
endif

if ENABLE_EXFAT
sbin_PROGRAMS += partclone.exfat
partclone_exfat_SOURCES=$(main_files) exfatclone.c exfatclone.h $(EXFATFS_SOURCE)
partclone_exfat_CFLAGS=-DEXFAT
endif

if ENABLE_FAT
sbin_PROGRAMS += partclone.fat
partclone_fat_SOURCES=$(main_files) fatclone.c fatclone.h
partclone_fat_CFLAGS=-DFAT
endif

sbin_PROGRAMS += partclone.ntfsfixboot
partclone_ntfsfixboot_SOURCES=ntfsfixboot.c
if ENABLE_NTFS
sbin_PROGRAMS += partclone.ntfs
partclone_ntfs_SOURCES=$(main_files) ntfsclone-ng.c ntfsclone-ng.h
if ENABLE_NTFS_3G
partclone_ntfs_CFLAGS=-DNTFS3G
partclone_ntfs_LDADD=-lntfs-3g
else
partclone_ntfs_CFLAGS=-DNTFS
partclone_ntfs_LDADD=-lntfs
endif
endif

if ENABLE_UFS
sbin_PROGRAMS += partclone.ufs
partclone_ufs_SOURCES=$(main_files) ufsclone.c ufsclone.h
partclone_ufs_CFLAGS=-DUFS -D_GNU_SOURCE
partclone_ufs_LDADD=-lufs -lbsd
endif

if ENABLE_VMFS
sbin_PROGRAMS += partclone.vmfs
partclone_vmfs_SOURCES=$(main_files) vmfsclone.c vmfsclone.h
partclone_vmfs_CFLAGS=-DVMFS -D_GNU_SOURCE $(UUID_CFLAGS)
partclone_vmfs_LDADD=-lvmfs -luuid

sbin_PROGRAMS += partclone.vmfs5
partclone_vmfs5_SOURCES=$(main_files) vmfs5clone.c vmfsclone.h
partclone_vmfs5_CFLAGS=-DVMFS -D_GNU_SOURCE $(UUID_CFLAGS)
partclone_vmfs5_LDADD=-lvmfs -luuid

sbin_PROGRAMS += partclone.fstype
partclone_fstype_SOURCES=fstype.c
partclone_fstype_CFLAGS=-DVMFS -D_GNU_SOURCE $(UUID_CFLAGS)
partclone_fstype_LDADD=-lvmfs -luuid

endif

if ENABLE_JFS
sbin_PROGRAMS += partclone.jfs
#partclone_jfs_SOURCES=$(main_files) jfs_devices.c jfs_devices.h jfsclone.c jfsclone.h
partclone_jfs_SOURCES=$(main_files) jfsclone.c jfsclone.h
partclone_jfs_CFLAGS=-DJFS
partclone_jfs_LDADD=-luuid -ljfs
endif

if ENABLE_BTRFS
sbin_PROGRAMS += partclone.btrfs
partclone_btrfs_SOURCES=$(main_files) btrfsclone.c btrfsclone.h $(BTRFS_SOURCE)
partclone_btrfs_CFLAGS=-DBTRFS
partclone_btrfs_LDADD=-luuid
endif

if ENABLE_MINIX
sbin_PROGRAMS += partclone.minix
partclone_minix_SOURCES=$(main_files) minixclone.c minixclone.h
partclone_minix_CFLAGS=-DMINIX
endif


# Extra
install-exec-hook:
if ENABLE_EXTFS
	$(LN_S) -f partclone.extfs $(DESTDIR)$(sbindir)/partclone.ext2
	$(LN_S) -f partclone.extfs $(DESTDIR)$(sbindir)/partclone.ext3
	$(LN_S) -f partclone.extfs $(DESTDIR)$(sbindir)/partclone.ext4
	$(LN_S) -f partclone.extfs $(DESTDIR)$(sbindir)/partclone.ext4dev
endif
if ENABLE_HFSP
	$(LN_S) -f partclone.hfsp $(DESTDIR)$(sbindir)/partclone.hfs+
	$(LN_S) -f partclone.hfsp $(DESTDIR)$(sbindir)/partclone.hfsplus
endif
if ENABLE_NTFS
	$(LN_S) -f partclone.ntfsfixboot $(DESTDIR)$(sbindir)/partclone.ntfsreloc
endif
if ENABLE_FAT
	$(LN_S) -f partclone.fat $(DESTDIR)$(sbindir)/partclone.fat12
	$(LN_S) -f partclone.fat $(DESTDIR)$(sbindir)/partclone.fat16
	$(LN_S) -f partclone.fat $(DESTDIR)$(sbindir)/partclone.fat32
	$(LN_S) -f partclone.fat $(DESTDIR)$(sbindir)/partclone.vfat
endif
if ENABLE_VMFS
	$(LN_S) -f partclone.vmfs $(DESTDIR)$(sbindir)/partclone.VMFS_volume_member
	$(LN_S) -f partclone.vmfs $(DESTDIR)$(sbindir)/partclone.vmfs3
#	$(LN_S) -f partclone.vmfs $(DESTDIR)$(sbindir)/partclone.vmfs5
endif

uninstall-local:
if ENABLE_EXTFS
	$(RM) -f $(sbindir)/partclone.ext4dev
	$(RM) -f $(sbindir)/partclone.ext4
	$(RM) -f $(sbindir)/partclone.ext3
	$(RM) -f $(sbindir)/partclone.ext2
endif
if ENABLE_HFSP
	$(RM) -f $(sbindir)/partclone.hfs+
	$(RM) -f $(sbindir)/partclone.hfsplus
endif
if ENABLE_FAT
	$(RM) -f $(sbindir)/partclone.fat12
	$(RM) -f $(sbindir)/partclone.fat16
	$(RM) -f $(sbindir)/partclone.fat32
	$(RM) -f $(sbindir)/partclone.vfat
endif
if ENABLE_NTFS
	$(RM) -f $(sbindir)/partclone.ntfsreloc
endif

if ENABLE_VMFS
	$(RM) -f $(sbindir)/partclone.VMFS_volume_member
endif

FORCE:
